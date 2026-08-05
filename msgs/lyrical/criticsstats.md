---
layout: default
title: "CriticsStats Message"
permalink: /msgs/lyrical/criticsstats.html
---

# CriticsStats Message

**Package:** `nav2_msgs`  
**Category:** Controller Messages

Statistics from controller critic plugins for debugging and tuning

## Message Definition

| Field | Type | Description |
|-------|------|-------------|
| `stamp` | `builtin_interfaces/Time` | Timestamp when statistics were recorded |
| `critics` | `string[]` | Names of the active critic plugins |
| `changed` | `bool[]` | Whether each critic's score changed since the last update |
| `costs_sum` | `float32[]` | Summed cost value for each critic |



## Usage Examples

### Python

```python
import rclpy
from rclpy.node import Node
from nav2_msgs.msg import CriticsStats

class CriticsStatsPublisher(Node):
    def __init__(self):
        super().__init__('criticsstats_publisher')
        self.publisher = self.create_publisher(CriticsStats, 'criticsstats', 10)
        
    def publish_message(self):
        msg = CriticsStats()
        msg.stamp = self.get_clock().now().to_msg()
        msg.critics = ['GoalCritic', 'ObstacleCritic', 'PathFollowCritic']
        msg.changed = [True, False, True]
        msg.costs_sum = [1.5, 0.0, 3.2]
        self.publisher.publish(msg)
```

### C++

```cpp
#include "rclcpp/rclcpp.hpp"
#include "nav2_msgs/msg/critics_stats.hpp"

class CriticsStatsPublisher : public rclcpp::Node
{
public:
    CriticsStatsPublisher() : Node("criticsstats_publisher")
    {
        publisher_ = create_publisher<nav2_msgs::msg::CriticsStats>("criticsstats", 10);
    }

    void publish_message()
    {
        auto msg = nav2_msgs::msg::CriticsStats();
        msg.stamp = now();
        msg.critics = {"GoalCritic", "ObstacleCritic", "PathFollowCritic"};
        msg.changed = {true, false, true};
        msg.costs_sum = {1.5f, 0.0f, 3.2f};
        publisher_->publish(msg);
    }

private:
    rclcpp::Publisher<nav2_msgs::msg::CriticsStats>::SharedPtr publisher_;
};
```

## Related Messages

- [All Controller Messages](/lyrical/msgs/index.html#controller-messages)
- [Message API Overview](/lyrical/msgs/index.html)
- [Nav2 C++ API Documentation](/lyrical/html/index.html)
