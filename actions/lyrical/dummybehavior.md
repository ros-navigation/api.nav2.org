---
layout: default
title: "DummyBehavior Action"
permalink: /actions/lyrical/dummybehavior.html
---

# DummyBehavior Action

**Package:** `nav2_msgs`  
**Category:** Behaviors

Test and development utility behavior for behavior tree validation

## Message Definitions

### Goal Message

| Field | Type | Description |
|-------|------|-------------|
| `command` | `std_msgs/String` | Command string for the dummy behavior |


### Result Message

| Field | Type | Description |
|-------|------|-------------|
| `total_elapsed_time` | `builtin_interfaces/Duration` | Total time elapsed during behavior execution |
| `error_code` | `uint16` | Numeric error code indicating specific failure reason |
| `error_msg` | `string` | Human-readable error message describing what went wrong during action execution |


### Feedback Message

No feedback fields defined for this action.



## Usage Examples

### Python

```python
import rclpy
from rclpy.node import Node
from rclpy.action import ActionClient
from nav2_msgs.action import DummyBehavior

class Nav2ActionClient(Node):
    def __init__(self):
        super().__init__('nav2_action_client')
        self.action_client = ActionClient(self, DummyBehavior, 'dummy_behavior')
        
    def send_goal(self):
        goal_msg = DummyBehavior.Goal()
        goal_msg.command.data = 'test_command'
        
        self.action_client.wait_for_server()
        future = self.action_client.send_goal_async(
            goal_msg, feedback_callback=self.feedback_callback)
        return future
        
    def feedback_callback(self, feedback_msg):
        self.get_logger().info(f'Received feedback: {feedback_msg.feedback}')
```

### C++

```cpp
#include "rclcpp/rclcpp.hpp"
#include "rclcpp_action/rclcpp_action.hpp"
#include "nav2_msgs/action/dummy_behavior.hpp"

class Nav2ActionClient : public rclcpp::Node
{
public:
    using DummyBehaviorAction = nav2_msgs::action::DummyBehavior;
    using GoalHandle = rclcpp_action::ClientGoalHandle<DummyBehaviorAction>;

    Nav2ActionClient() : Node("nav2_action_client")
    {
        action_client_ = rclcpp_action::create_client<DummyBehaviorAction>(
            this, "dummy_behavior");
    }

    void send_goal()
    {
        auto goal_msg = DummyBehaviorAction::Goal();
        goal_msg.command.data = "test_command";
        
        action_client_->wait_for_action_server();
        
        auto send_goal_options = rclcpp_action::Client<DummyBehaviorAction>::SendGoalOptions();
        send_goal_options.feedback_callback = 
            std::bind(&Nav2ActionClient::feedback_callback, this, 
                     std::placeholders::_1, std::placeholders::_2);
        
        action_client_->async_send_goal(goal_msg, send_goal_options);
    }

private:
    rclcpp_action::Client<DummyBehaviorAction>::SharedPtr action_client_;
    
    void feedback_callback(GoalHandle::SharedPtr, 
                          const std::shared_ptr<const DummyBehaviorAction::Feedback> feedback)
    {
        RCLCPP_INFO(this->get_logger(), "Received feedback");
    }
};
```

## Related Actions

- [All Behavior Actions](/actions/lyrical/index.html#behaviors)
- [Action API Overview](/actions/lyrical/index.html)
- [Nav2 C++ API Documentation](/lyrical/html/index.html)
