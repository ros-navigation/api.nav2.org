---
layout: default
title: "FollowObject Action"
permalink: /actions/rolling/followobject.html
---

# FollowObject Action

**Package:** `nav2_msgs`  
**Category:** Object Following

Follow a detected object using pose tracking or TF frame tracking

## Message Definitions

### Goal Message

| Field | Type | Description |
|-------|------|-------------|
| `pose_topic` | `string` | Topic to publish the pose of the object to follow |
| `tracked_frame` | `string` | Target TF frame to follow (optional, used if pose_topic is not set) |
| `max_duration` | `builtin_interfaces/Duration` | Maximum duration for the object following task |


### Result Message

| Field | Type | Description |
|-------|------|-------------|
| `NONE` | `uint16` | Success status code indicating the action completed without errors |
| `GOAL_REJECTED` | `uint16` | Error code indicating the goal was rejected by the server |
| `SEND_GOAL_FAILURE` | `uint16` | Error code indicating failure to send the goal |
| `TF_ERROR` | `uint16` | Error code indicating a transform/localization failure |
| `FAILED_TO_DETECT_OBJECT` | `uint16` | Error code indicating the target object could not be detected |
| `FAILED_TO_CONTROL` | `uint16` | Error code indicating control system failure during following |
| `TIMEOUT` | `uint16` | Error code indicating the action exceeded its maximum allowed time |
| `UNKNOWN` | `uint16` | Generic error code for unexpected or unclassified failures |
| `total_elapsed_time` | `builtin_interfaces/Duration` | Total time elapsed during object following |
| `error_code` | `uint16` | Contextual error code, if any |
| `num_retries` | `uint16` | Number of retries attempted |
| `error_msg` | `string` | Human-readable error message describing what went wrong during action execution |


### Feedback Message

| Field | Type | Description |
|-------|------|-------------|
| `NONE` | `uint16` | No active state |
| `INITIAL_PERCEPTION` | `uint16` | Initial object detection phase |
| `CONTROLLING` | `uint16` | Actively following the object |
| `STOPPING` | `uint16` | Decelerating to stop |
| `RETRY` | `uint16` | Retrying after a failure |
| `state` | `uint16` | Current following state |
| `following_time` | `builtin_interfaces/Duration` | Time elapsed since following began |
| `num_retries` | `uint16` | Number of retries attempted |



## Usage Examples

### Python

```python
import rclpy
from rclpy.node import Node
from rclpy.action import ActionClient
from nav2_msgs.action import FollowObject

class Nav2ActionClient(Node):
    def __init__(self):
        super().__init__('nav2_action_client')
        self.action_client = ActionClient(self, FollowObject, 'follow_object')
        
    def send_goal(self):
        goal_msg = FollowObject.Goal()
        goal_msg.pose_topic = '/detected_object_pose'
        # Alternative: track a TF frame instead of a pose topic
        # goal.tracked_frame = 'target_object'
        goal_msg.max_duration = Duration(seconds=60.0)
        
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
#include "nav2_msgs/action/follow_object.hpp"

class Nav2ActionClient : public rclcpp::Node
{
public:
    using FollowObjectAction = nav2_msgs::action::FollowObject;
    using GoalHandle = rclcpp_action::ClientGoalHandle<FollowObjectAction>;

    Nav2ActionClient() : Node("nav2_action_client")
    {
        action_client_ = rclcpp_action::create_client<FollowObjectAction>(
            this, "follow_object");
    }

    void send_goal()
    {
        auto goal_msg = FollowObjectAction::Goal();
        goal_msg.pose_topic = "/detected_object_pose";
        // Alternative: track a TF frame instead of a pose topic
        // goal_msg.tracked_frame = "target_object";
        goal_msg.max_duration = rclcpp::Duration::from_seconds(60.0);
        
        action_client_->wait_for_action_server();
        
        auto send_goal_options = rclcpp_action::Client<FollowObjectAction>::SendGoalOptions();
        send_goal_options.feedback_callback = 
            std::bind(&Nav2ActionClient::feedback_callback, this, 
                     std::placeholders::_1, std::placeholders::_2);
        
        action_client_->async_send_goal(goal_msg, send_goal_options);
    }

private:
    rclcpp_action::Client<FollowObjectAction>::SharedPtr action_client_;
    
    void feedback_callback(GoalHandle::SharedPtr, 
                          const std::shared_ptr<const FollowObjectAction::Feedback> feedback)
    {
        RCLCPP_INFO(this->get_logger(), "Received feedback");
    }
};
```

## Related Actions

- [All Object Following Actions](/actions/rolling/index.html)
- [Action API Overview](/actions/rolling/index.html)
- [Nav2 C++ API Documentation](/rolling/html/index.html)
