---
layout: default
title: "AddExclusionZone Service"
permalink: /srvs/lyrical/addexclusionzone.html
---

# AddExclusionZone Service

**Package:** `nav2_msgs`  
**Category:** Collision Monitor Services

Add an exclusion zone to a collision monitor or detector source at runtime

## Message Definitions

### Request Message

| Field | Type | Description |
|-------|------|-------------|
| `zone` | `nav2_msgs/ExclusionZoneDescription` | Description of the exclusion zone to add |


### Response Message

| Field | Type | Description |
|-------|------|-------------|
| `success` | `bool` | Whether the zone was added successfully |
| `message` | `string` | Status message with details on success or failure |



## Usage Examples

### Python

```python
import rclpy
from rclpy.node import Node
from nav2_msgs.srv import AddExclusionZone

class AddExclusionZoneClient(Node):
    def __init__(self):
        super().__init__('add_exclusion_zone_client')
        self.client = self.create_client(AddExclusionZone, 'add_exclusion_zone')
        
    def send_request(self):
        request = AddExclusionZone.Request()
        request.zone.zone_name = 'restricted_area'
        request.zone.type = 'polygon'
        request.zone.frame_id = 'map'
        request.zone.points = [
            Point32(x=1.0, y=1.0, z=0.0),
            Point32(x=1.0, y=3.0, z=0.0),
            Point32(x=3.0, y=3.0, z=0.0),
            Point32(x=3.0, y=1.0, z=0.0)]
        request.zone.enabled = True
        
        self.client.wait_for_service()
        future = self.client.call_async(request)
        return future

def main():
    rclpy.init()
    client = AddExclusionZoneClient()
    
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
#include "nav2_msgs/srv/add_exclusion_zone.hpp"

class AddExclusionZoneClient : public rclcpp::Node
{
public:
    AddExclusionZoneClient() : Node("add_exclusion_zone_client")
    {
        client_ = create_client<nav2_msgs::srv::AddExclusionZone>("add_exclusion_zone");
    }

    void send_request()
    {
        auto request = std::make_shared<nav2_msgs::srv::AddExclusionZone::Request>();
        request->zone.zone_name = "restricted_area";
        request->zone.type = "polygon";
        request->zone.frame_id = "map";
        geometry_msgs::msg::Point32 p1, p2, p3, p4;
        p1.x = 1.0; p1.y = 1.0;
        p2.x = 1.0; p2.y = 3.0;
        p3.x = 3.0; p3.y = 3.0;
        p4.x = 3.0; p4.y = 1.0;
        request->zone.points = {p1, p2, p3, p4};
        request->zone.enabled = true;

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
    rclcpp::Client<nav2_msgs::srv::AddExclusionZone>::SharedPtr client_;
};
```

## Related Services

- [All Collision Monitor Services](/lyrical/srvs/index.html#collision-monitor-services)
- [Service API Overview](/lyrical/srvs/index.html)
- [Nav2 C++ API Documentation](/lyrical/html/index.html)
