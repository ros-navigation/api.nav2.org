---
layout: default
title: "Toggle Service"
permalink: /srvs/rolling/toggle.html
---

# Toggle Service

**Package:** `nav2_msgs`  
**Category:** Utility Services

Enable or disable a Nav2 component at runtime

## Message Definitions

### Request Message

| Field | Type | Description |
|-------|------|-------------|
| `enable` | `bool` | Whether to enable (true) or disable (false) the component |


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
from nav2_msgs.srv import Toggle

class ToggleClient(Node):
    def __init__(self):
        super().__init__('toggle_client')
        self.client = self.create_client(Toggle, 'toggle')
        
    def send_request(self):
        request = Toggle.Request()
        request.enable = True
        
        self.client.wait_for_service()
        future = self.client.call_async(request)
        return future

def main():
    rclpy.init()
    client = ToggleClient()
    
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
#include "nav2_msgs/srv/toggle.hpp"

class ToggleClient : public rclcpp::Node
{
public:
    ToggleClient() : Node("toggle_client")
    {
        client_ = create_client<nav2_msgs::srv::Toggle>("toggle");
    }

    void send_request()
    {
        auto request = std::make_shared<nav2_msgs::srv::Toggle::Request>();
        request->enable = true;

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
    rclcpp::Client<nav2_msgs::srv::Toggle>::SharedPtr client_;
};
```

## Related Services

- [All Utility Services](/rolling/srvs/index.html#utility-services)
- [Service API Overview](/rolling/srvs/index.html)
- [Nav2 C++ API Documentation](/rolling/html/index.html)
