---
layout: default
title: "Nav2 Message APIs - Rolling"
permalink: /rolling/msgs/
---

# Nav2 Message APIs - Rolling

This page documents the ROS Message APIs available in Nav2 for the rolling distribution. These messages provide data structures for navigation tasks, sensor data, and system status.

## Available Messages (24 total)


### Costmap Messages

<div class="action-grid">
  <div class="action-card">
    <h4><a href="/rolling/msgs/costmap.html">Costmap</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Occupancy grid representation for navigation planning with cost values</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/costmapfilterinfo.html">CostmapFilterInfo</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Filter information for costmap layers and processing</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/costmapmetadata.html">CostmapMetaData</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Metadata information for costmap including dimensions and resolution</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/costmapupdate.html">CostmapUpdate</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Update message containing changed regions of a costmap</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/voxelgrid.html">VoxelGrid</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">3D voxel grid representation for obstacle detection and mapping</p>
  </div>
</div>

### Behavior Tree Messages

<div class="action-grid">
  <div class="action-card">
    <h4><a href="/rolling/msgs/behaviortreelog.html">BehaviorTreeLog</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Logging information from behavior tree execution</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/behaviortreestatuschange.html">BehaviorTreeStatusChange</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Status change events from behavior tree nodes</p>
  </div>
</div>

### Localization Messages

<div class="action-grid">
  <div class="action-card">
    <h4><a href="/rolling/msgs/particle.html">Particle</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Single particle hypothesis with pose and weight for particle filter localization</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/particlecloud.html">ParticleCloud</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Collection of particles representing pose distribution in particle filter</p>
  </div>
</div>

### Route Planning Messages

<div class="action-grid">
  <div class="action-card">
    <h4><a href="/rolling/msgs/edgecost.html">EdgeCost</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Cost information for route graph edges</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/route.html">Route</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Complete route plan with waypoints and metadata</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/routeedge.html">RouteEdge</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Connection between route nodes with traversal cost</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/routenode.html">RouteNode</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Individual waypoint node in a route graph</p>
  </div>
</div>

### Controller Messages

<div class="action-grid">
  <div class="action-card">
    <h4><a href="/rolling/msgs/criticsstats.html">CriticsStats</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Statistics from controller critic plugins for debugging and tuning</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/trackingfeedback.html">TrackingFeedback</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Real-time tracking error feedback from the Nav2 controller for path following</p>
  </div>
</div>

### Vector Map Messages

<div class="action-grid">
  <div class="action-card">
    <h4><a href="/rolling/msgs/circleobject.html">CircleObject</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Circle object for vector map representation on costmaps</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/polygonobject.html">PolygonObject</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Polygon object for vector map representation on costmaps</p>
  </div>
</div>

### Collision Detection Messages

<div class="action-grid">
  <div class="action-card">
    <h4><a href="/rolling/msgs/collisiondetectorstate.html">CollisionDetectorState</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">State information from collision detection systems</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/collisionmonitorstate.html">CollisionMonitorState</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Monitoring state for collision avoidance systems</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/exclusionzonedescription.html">ExclusionZoneDescription</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Description of an exclusion zone for the collision monitor or detector</p>
  </div>
</div>

### Trajectory Messages

<div class="action-grid">
  <div class="action-card">
    <h4><a href="/rolling/msgs/speedlimit.html">SpeedLimit</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Speed limit information for navigation areas</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/trajectory.html">Trajectory</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Time-parameterized path with poses and velocities</p>
  </div>
  <div class="action-card">
    <h4><a href="/rolling/msgs/trajectorypoint.html">TrajectoryPoint</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Single point in a trajectory with pose, velocity, and timing</p>
  </div>
</div>

### Waypoint Messages

<div class="action-grid">
  <div class="action-card">
    <h4><a href="/rolling/msgs/waypointstatus.html">WaypointStatus</a></h4>
    <p class="action-package">Package: nav2_msgs</p>
    <p class="action-description">Status information for waypoint navigation tasks</p>
  </div>
</div>


## Related Documentation

- [Nav2 Action APIs](/actions/rolling/index.html)
- [Nav2 Service APIs](/srvs/rolling/index.html)
- [Nav2 C++ API Documentation](/rolling/html/index.html)
- [Nav2 Official Documentation](https://nav2.org/)
