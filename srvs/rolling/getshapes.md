---
layout: default
title: "GetShapes Service"
permalink: /srvs/rolling/getshapes.html
---

# GetShapes Service

**Package:** `nav2_msgs`  
**Category:** Vector Map Services

Retrieve vector objects currently applied on the costmap

## Message Definitions

### Request Message

No fields (empty request)


### Response Message

| Field | Type | Description |
|-------|------|-------------|
| `circles` | `CircleObject[]` | Array of circle objects currently applied on the map |
| `polygons` | `PolygonObject[]` | Array of polygon objects currently applied on the map |



## Usage Examples

### Python

```python
import rclpy
from rclpy.node import Node
from nav2_msgs.srv import GetShapes

class GetShapesClient(Node):
    def __init__(self):
        super().__init__('get_shapes_client')
        self.client = self.create_client(GetShapes, 'get_shapes')
        
    def send_request(self):
        request = GetShapes.Request()
        
        self.client.wait_for_service()
        future = self.client.call_async(request)
        return future

def main():
    rclpy.init()
    client = GetShapesClient()
    
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
#include "nav2_msgs/srv/get_shapes.hpp"

class GetShapesClient : public rclcpp::Node
{
public:
    GetShapesClient() : Node("get_shapes_client")
    {
        client_ = create_client<nav2_msgs::srv::GetShapes>("get_shapes");
    }

    void send_request()
    {
        auto request = std::make_shared<nav2_msgs::srv::GetShapes::Request>();

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
    rclcpp::Client<nav2_msgs::srv::GetShapes>::SharedPtr client_;
};
```

## Related Services

- [All Vector Map Services](/rolling/srvs/index.html#vector-map-services)
- [Service API Overview](/rolling/srvs/index.html)
- [Nav2 C++ API Documentation](/rolling/html/index.html)
