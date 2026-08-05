---
layout: default
title: "RemoveShapes Service"
permalink: /srvs/lyrical/removeshapes.html
---

# RemoveShapes Service

**Package:** `nav2_msgs`  
**Category:** Vector Map Services

Remove vector objects from the costmap by UUID or remove all

## Message Definitions

### Request Message

| Field | Type | Description |
|-------|------|-------------|
| `all_objects` | `bool` | If true, remove all vector objects from the map |
| `uuids` | `unique_identifier_msgs/UUID[]` | Specific object UUIDs to remove (used when all_objects is false) |


### Response Message

| Field | Type | Description |
|-------|------|-------------|
| `success` | `bool` | Whether the objects were removed successfully |



## Usage Examples

### Python

```python
import rclpy
from rclpy.node import Node
from nav2_msgs.srv import RemoveShapes

class RemoveShapesClient(Node):
    def __init__(self):
        super().__init__('remove_shapes_client')
        self.client = self.create_client(RemoveShapes, 'remove_shapes')
        
    def send_request(self):
        request = RemoveShapes.Request()
        request.all_objects = True
        
        self.client.wait_for_service()
        future = self.client.call_async(request)
        return future

def main():
    rclpy.init()
    client = RemoveShapesClient()
    
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
#include "nav2_msgs/srv/remove_shapes.hpp"

class RemoveShapesClient : public rclcpp::Node
{
public:
    RemoveShapesClient() : Node("remove_shapes_client")
    {
        client_ = create_client<nav2_msgs::srv::RemoveShapes>("remove_shapes");
    }

    void send_request()
    {
        auto request = std::make_shared<nav2_msgs::srv::RemoveShapes::Request>();
        request->all_objects = true;

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
    rclcpp::Client<nav2_msgs::srv::RemoveShapes>::SharedPtr client_;
};
```

## Related Services

- [All Vector Map Services](/lyrical/srvs/index.html#vector-map-services)
- [Service API Overview](/lyrical/srvs/index.html)
- [Nav2 C++ API Documentation](/lyrical/html/index.html)
