---
layout: default
title: "Nav2 Service APIs - Lyrical"
permalink: /srvs/lyrical/
---

# Nav2 Service APIs - Lyrical

This page documents the ROS Service APIs available in Nav2 for the lyrical distribution. These services provide request-response interfaces for navigation configuration, system control, and data queries.

## Available Services (20 total)


### Costmap Services

<div class="service-grid">
  <div class="service-card">
    <h4><a href="/srvs/lyrical/clearcostmaparoundpose.html">ClearCostmapAroundPose</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Clear costmap within a specified distance around a given pose</p>
  </div>
  <div class="service-card">
    <h4><a href="/srvs/lyrical/clearcostmaparoundrobot.html">ClearCostmapAroundRobot</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Clear costmap within a specified distance around the robot's current position</p>
  </div>
  <div class="service-card">
    <h4><a href="/srvs/lyrical/clearcostmapexceptregion.html">ClearCostmapExceptRegion</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Clear entire costmap except for a specified rectangular region</p>
  </div>
  <div class="service-card">
    <h4><a href="/srvs/lyrical/clearentirecostmap.html">ClearEntireCostmap</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Clear the entire costmap, resetting all cells to free space</p>
  </div>
  <div class="service-card">
    <h4><a href="/srvs/lyrical/getcostmap.html">GetCostmap</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Retrieve the entire costmap as an occupancy grid</p>
  </div>
  <div class="service-card">
    <h4><a href="/srvs/lyrical/getcosts.html">GetCosts</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Retrieve costmap cost values at specified poses</p>
  </div>
</div>

### Route Planning Services

<div class="service-grid">
  <div class="service-card">
    <h4><a href="/srvs/lyrical/dynamicedges.html">DynamicEdges</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Dynamically modify route graph edges during navigation</p>
  </div>
  <div class="service-card">
    <h4><a href="/srvs/lyrical/setroutegraph.html">SetRouteGraph</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Load a new route graph from a specified file path</p>
  </div>
</div>

### Map Services

<div class="service-grid">
  <div class="service-card">
    <h4><a href="/srvs/lyrical/loadmap.html">LoadMap</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Load a map from a specified URL or file path</p>
  </div>
  <div class="service-card">
    <h4><a href="/srvs/lyrical/savemap.html">SaveMap</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Save the current map to a specified file location</p>
  </div>
</div>

### Docking Services

<div class="service-grid">
  <div class="service-card">
    <h4><a href="/srvs/lyrical/reloaddockdatabase.html">ReloadDockDatabase</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Reload the docking database with updated dock configurations</p>
  </div>
</div>

### Lifecycle Services

<div class="service-grid">
  <div class="service-card">
    <h4><a href="/srvs/lyrical/managelifecyclenodes.html">ManageLifecycleNodes</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Control lifecycle states of Nav2 nodes (startup, shutdown, pause, etc.)</p>
  </div>
</div>

### Collision Monitor Services

<div class="service-grid">
  <div class="service-card">
    <h4><a href="/srvs/lyrical/addexclusionzone.html">AddExclusionZone</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Add an exclusion zone to a collision monitor or detector source at runtime</p>
  </div>
  <div class="service-card">
    <h4><a href="/srvs/lyrical/removeexclusionzone.html">RemoveExclusionZone</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Remove exclusion zone(s) from a collision monitor or detector source at runtime</p>
  </div>
</div>

### Vector Map Services

<div class="service-grid">
  <div class="service-card">
    <h4><a href="/srvs/lyrical/addshapes.html">AddShapes</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Add or update vector objects (circles and polygons) on the costmap</p>
  </div>
  <div class="service-card">
    <h4><a href="/srvs/lyrical/getshapes.html">GetShapes</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Retrieve vector objects currently applied on the costmap</p>
  </div>
  <div class="service-card">
    <h4><a href="/srvs/lyrical/removeshapes.html">RemoveShapes</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Remove vector objects from the costmap by UUID or remove all</p>
  </div>
</div>

### Utility Services

<div class="service-grid">
  <div class="service-card">
    <h4><a href="/srvs/lyrical/toggle.html">Toggle</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Enable or disable a Nav2 component at runtime</p>
  </div>
</div>

### Validation Services

<div class="service-grid">
  <div class="service-card">
    <h4><a href="/srvs/lyrical/ispathvalid.html">IsPathValid</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Validate whether a given path is collision-free and traversable</p>
  </div>
</div>

### Localization Services

<div class="service-grid">
  <div class="service-card">
    <h4><a href="/srvs/lyrical/setinitialpose.html">SetInitialPose</a></h4>
    <p class="service-package">Package: nav2_msgs</p>
    <p class="service-description">Set the initial pose estimate for robot localization</p>
  </div>
</div>


## Related Documentation

- [Nav2 Action APIs](/actions/lyrical/index.html)
- [Nav2 Message APIs](/msgs/lyrical/index.html)
- [Nav2 C++ API Documentation](/lyrical/html/index.html)
- [Nav2 Official Documentation](https://nav2.org/)
