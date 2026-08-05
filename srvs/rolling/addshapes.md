---
layout: default
title: "AddShapes Service"
permalink: /srvs/rolling/addshapes.html
---

# AddShapes Service

**Package:** `nav2_msgs`  
**Category:** Vector Map Services

Add or update vector objects (circles and polygons) on the costmap

## Message Definitions

### Request Message

| Field | Type | Description |
|-------|------|-------------|
| `circles` | `CircleObject[]` | Array of circle objects to add or update on the map |
| `polygons` | `PolygonObject[]` | Array of polygon objects to add or update on the map |


### Response Message

| Field | Type | Description |
|-------|------|-------------|
| `success` | `bool` | Whether the objects were added successfully |



## Usage Examples

### Python

```python
import rclpy
from rclpy.node import Node
from nav2_msgs.srv import AddShapes

class AddShapesClient(Node):
    def __init__(self):
        super().__init__('add_shapes_client')
        self.client = self.create_client(AddShapes, 'add_shapes')
        
    def send_request(self):
        request = AddShapes.Request()
        circle = CircleObject()
        circle.center = Point32(x=2.0, y=3.0, z=0.0)
        circle.radius = 0.5
        circle.fill = True
        circle.value = 254
        request.circles = [circle]
        
        self.client.wait_for_service()
        future = self.client.call_async(request)
        return future

def main():
    rclpy.init()
    client = AddShapesClient()
    
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
#include "nav2_msgs/srv/add_shapes.hpp"

class AddShapesClient : public rclcpp::Node
{
public:
    AddShapesClient() : Node("add_shapes_client")
    {
        client_ = create_client<nav2_msgs::srv::AddShapes>("add_shapes");
    }

    void send_request()
    {
        auto request = std::make_shared<nav2_msgs::srv::AddShapes::Request>();
        nav2_msgs::msg::CircleObject circle;
        circle.center.x = 2.0;
        circle.center.y = 3.0;
        circle.radius = 0.5;
        circle.fill = true;
        circle.value = 254;
        request->circles = {circle};

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
    rclcpp::Client<nav2_msgs::srv::AddShapes>::SharedPtr client_;
};
```

## Related Services

- [All Vector Map Services](/rolling/srvs/index.html#vector-map-services)
- [Service API Overview](/rolling/srvs/index.html)
- [Nav2 C++ API Documentation](/rolling/html/index.html)
