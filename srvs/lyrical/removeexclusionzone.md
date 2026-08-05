---
layout: default
title: "RemoveExclusionZone Service"
permalink: /srvs/lyrical/removeexclusionzone.html
---

# RemoveExclusionZone Service

**Package:** `nav2_msgs`  
**Category:** Collision Monitor Services

Remove exclusion zone(s) from a collision monitor or detector source at runtime

## Message Definitions

### Request Message

| Field | Type | Description |
|-------|------|-------------|
| `zone_name` | `string` | Name of the exclusion zone to remove (ignored if remove_all is true) |
| `remove_all` | `bool` | If true, remove all zones from this source (default: false) |


### Response Message

| Field | Type | Description |
|-------|------|-------------|
| `success` | `bool` | Whether the operation completed successfully |
| `message` | `string` | Status message with details on success or failure |



## Usage Examples

### Python

```python
import rclpy
from rclpy.node import Node
from nav2_msgs.srv import RemoveExclusionZone

class RemoveExclusionZoneClient(Node):
    def __init__(self):
        super().__init__('remove_exclusion_zone_client')
        self.client = self.create_client(RemoveExclusionZone, 'remove_exclusion_zone')
        
    def send_request(self):
        request = RemoveExclusionZone.Request()
        request.zone_name = 'my_zone'
        request.remove_all = False
        
        self.client.wait_for_service()
        future = self.client.call_async(request)
        return future

def main():
    rclpy.init()
    client = RemoveExclusionZoneClient()
    
    future = client.send_request()
    rclpy.spin_until_future_complete(client, future)
    
    if future.result():
        client.get_logger().info('Service call completed')
    else:
        client.get_logger().error('Service call failed')
        
    client.destroy_node()
    rclpy.shutdown()
```

### C++

```cpp
#include "rclcpp/rclcpp.hpp"
#include "nav2_msgs/srv/remove_exclusion_zone.hpp"

class RemoveExclusionZoneClient : public rclcpp::Node
{
public:
    RemoveExclusionZoneClient() : Node("remove_exclusion_zone_client")
    {
        client_ = create_client<nav2_msgs::srv::RemoveExclusionZone>("remove_exclusion_zone");
    }

    void send_request()
    {
        auto request = std::make_shared<nav2_msgs::srv::RemoveExclusionZone::Request>();
        request->zone_name = "my_zone";
        request->remove_all = false;

        client_->wait_for_service();
        
        auto result_future = client_->async_send_request(request);
        if (rclcpp::spin_until_future_complete(shared_from_this(), result_future) ==
            rclcpp::FutureReturnCode::SUCCESS)
        {
            RCLCPP_INFO(get_logger(), "Service call completed");
        }
        else
        {
            RCLCPP_ERROR(get_logger(), "Service call failed");
        }
    }

private:
    rclcpp::Client<nav2_msgs::srv::RemoveExclusionZone>::SharedPtr client_;
};
```

## Related Services

- [All Collision Monitor Services](/lyrical/srvs/index.html#collision-monitor-services)
- [Service API Overview](/lyrical/srvs/index.html)
- [Nav2 C++ API Documentation](/lyrical/html/index.html)
