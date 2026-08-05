---
layout: default
title: "ExclusionZoneDescription Message"
permalink: /msgs/rolling/exclusionzonedescription.html
---

# ExclusionZoneDescription Message

**Package:** `nav2_msgs`  
**Category:** Collision Monitor Messages

Description of an exclusion zone for the collision monitor or detector

## Message Definition

| Field | Type | Description |
|-------|------|-------------|
| `zone_name` | `string` | Unique name for the exclusion zone within the source |
| `type` | `string` | Zone geometry type: "polygon" or "circle" |
| `frame_id` | `string` | TF frame the zone is anchored to (empty = base_frame_id) |
| `points` | `geometry_msgs/Point32[]` | Polygon vertices in frame_id (ignored for circle type) |
| `radius` | `float64` | Circle radius in metres (ignored for polygon type) |
| `min_height` | `float64` | Lower z-bound in base frame (default: -DBL_MAX) |
| `max_height` | `float64` | Upper z-bound in base frame (default: +DBL_MAX) |
| `enabled` | `bool` | Whether the zone is active on creation |
| `visualize` | `bool` | Whether to publish the zone polygon for RViz visualization |
| `frame_hold_timeout` | `float64` | Extra staleness allowance in seconds for TF lookups |



## Usage Examples

### Python

```python
import rclpy
from rclpy.node import Node
from nav2_msgs.msg import ExclusionZoneDescription
from geometry_msgs.msg import Point32

class ExclusionZoneDescriptionPublisher(Node):
    def __init__(self):
        super().__init__('exclusionzonedescription_publisher')
        self.publisher = self.create_publisher(ExclusionZoneDescription, 'exclusionzonedescription', 10)
        
    def publish_message(self):
        msg = ExclusionZoneDescription()
        msg.zone_name = 'loading_dock_zone'
        msg.type = 'polygon'
        msg.frame_id = 'map'
        p1 = Point32(x=1.0, y=1.0, z=0.0)
        p2 = Point32(x=3.0, y=1.0, z=0.0)
        p3 = Point32(x=3.0, y=3.0, z=0.0)
        p4 = Point32(x=1.0, y=3.0, z=0.0)
        msg.points = [p1, p2, p3, p4]
        msg.radius = 0.0
        msg.min_height = -float('inf')
        msg.max_height = float('inf')
        msg.enabled = True
        msg.visualize = True
        msg.frame_hold_timeout = 0.5
        self.publisher.publish(msg)
```

### C++

```cpp
#include "rclcpp/rclcpp.hpp"
#include "nav2_msgs/msg/exclusion_zone_description.hpp"
#include "geometry_msgs/msg/point32.hpp"

class ExclusionZoneDescriptionPublisher : public rclcpp::Node
{
public:
    ExclusionZoneDescriptionPublisher() : Node("exclusionzonedescription_publisher")
    {
        publisher_ = create_publisher<nav2_msgs::msg::ExclusionZoneDescription>(
            "exclusionzonedescription", 10);
    }

    void publish_message()
    {
        auto msg = nav2_msgs::msg::ExclusionZoneDescription();
        msg.zone_name = "loading_dock_zone";
        msg.type = "polygon";
        msg.frame_id = "map";
        geometry_msgs::msg::Point32 p1, p2, p3, p4;
        p1.x = 1.0; p1.y = 1.0; p1.z = 0.0;
        p2.x = 3.0; p2.y = 1.0; p2.z = 0.0;
        p3.x = 3.0; p3.y = 3.0; p3.z = 0.0;
        p4.x = 1.0; p4.y = 3.0; p4.z = 0.0;
        msg.points = {p1, p2, p3, p4};
        msg.radius = 0.0;
        msg.min_height = -std::numeric_limits<double>::max();
        msg.max_height = std::numeric_limits<double>::max();
        msg.enabled = true;
        msg.visualize = true;
        msg.frame_hold_timeout = 0.5;
        publisher_->publish(msg);
    }

private:
    rclcpp::Publisher<nav2_msgs::msg::ExclusionZoneDescription>::SharedPtr publisher_;
};
```

## Related Messages

- [All Collision Monitor Messages](/rolling/msgs/index.html#collision-monitor-messages)
- [Message API Overview](/rolling/msgs/index.html)
- [Nav2 C++ API Documentation](/rolling/html/index.html)
