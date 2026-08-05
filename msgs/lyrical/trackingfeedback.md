---
layout: default
title: "TrackingFeedback Message"
permalink: /msgs/lyrical/trackingfeedback.html
---

# TrackingFeedback Message

**Package:** `nav2_msgs`  
**Category:** Controller Messages

Real-time tracking error feedback from the Nav2 controller for path following

## Message Definition

| Field | Type | Description |
|-------|------|-------------|
| `header` | `std_msgs/Header` | Standard ROS header with timestamp and frame |
| `position_tracking_error` | `float32` | Signed cross-track error. Positive means robot is to the left of the path, negative to the right |
| `heading_tracking_error` | `float32` | Signed heading error. Positive means robot heading is rotated to the right of the path direction, negative to the left |
| `current_path_index` | `uint32` | Index of the closest point on the path to the robot |
| `robot_pose` | `geometry_msgs/PoseStamped` | Current robot pose |
| `distance_to_goal` | `float32` | Distance from the robot to the final goal position in meters |
| `speed` | `float32` | Current movement speed in meters per second |
| `remaining_path_length` | `float32` | Remaining path length to the goal in meters |



## Usage Examples

### Python

```python
import rclpy
from rclpy.node import Node
from nav2_msgs.msg import TrackingFeedback

class TrackingFeedbackPublisher(Node):
    def __init__(self):
        super().__init__('trackingfeedback_publisher')
        self.publisher = self.create_publisher(TrackingFeedback, 'trackingfeedback', 10)
        
    def publish_message(self):
        msg = TrackingFeedback()
        msg.header.stamp = self.get_clock().now().to_msg()
        msg.header.frame_id = 'base_link'
        msg.position_tracking_error = 0.05
        msg.heading_tracking_error = 0.02
        msg.current_path_index = 42
        # Set msg.robot_pose as needed
        msg.distance_to_goal = 3.5
        msg.speed = 0.5
        msg.remaining_path_length = 4.2
        self.publisher.publish(msg)
```

### C++

```cpp
#include "rclcpp/rclcpp.hpp"
#include "nav2_msgs/msg/tracking_feedback.hpp"

class TrackingFeedbackPublisher : public rclcpp::Node
{
public:
    TrackingFeedbackPublisher() : Node("trackingfeedback_publisher")
    {
        publisher_ = create_publisher<nav2_msgs::msg::TrackingFeedback>("trackingfeedback", 10);
    }

    void publish_message()
    {
        auto msg = nav2_msgs::msg::TrackingFeedback();
        msg.header.stamp = now();
        msg.header.frame_id = "base_link";
        msg.position_tracking_error = 0.05;
        msg.heading_tracking_error = 0.02;
        msg.current_path_index = 42;
        // Set msg.robot_pose as needed
        msg.distance_to_goal = 3.5;
        msg.speed = 0.5;
        msg.remaining_path_length = 4.2;
        publisher_->publish(msg);
    }

private:
    rclcpp::Publisher<nav2_msgs::msg::TrackingFeedback>::SharedPtr publisher_;
};
```

## Related Messages

- [All Controller Messages](/lyrical/msgs/index.html#controller-messages)
- [Message API Overview](/lyrical/msgs/index.html)
- [Nav2 C++ API Documentation](/lyrical/html/index.html)
