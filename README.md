# nav2_neo_localization

![neo_demo](https://github.com/user-attachments/assets/ca53ef5b-bb12-40a1-a50a-e418318f066d)

## Overview
**nav2_neo_localization** is a localization package for Nav2, derived from **neobotix/neo_localization2**. It has been modified and optimized for integration into the Nav2 Stack, providing accurate localization for autonomous robots. **This package can be used as a replacement for AMCL**, offering improved performance and flexibility in robot localization.

## XML configuration example
```
neo_localization:
  ros__parameters:
    base_frame: "base_link"
    odom_frame: "odom"
    # exponential low pass gain for localization update (0 to 1)
    #   (higher gain means odometry is less used / relied on)
    update_gain: 0.5

    # time based confidence gain when in 2D / 1D mode
    confidence_gain: 0.01

    # how many particles (samples) to spread (per update)
    sample_rate: 10

    # localization update rate [1/s]
    loc_update_rate: 100

    # map tile update rate [1/s]
    map_update_rate: 0.5

    # map tile size in pixels
    map_size: 1000

    # how often to downscale (half) the original map
    map_downscale: 0

    # how many 3x3 gaussian smoothing iterations are applied to the map
    num_smooth: 0

    # minimum score for valid localization (otherwise 0D mode)
    #    higher values make it go into 0D mode earlier
    min_score: 0.2

    # odometry error in x and y [m/m] [1]
    #    how fast to increase particle spread when in 1D / 0D mode
    odometry_std_xy: 0.01

    # odometry error in yaw angle [rad/rad] [1]
    #    how fast to increase particle spread when in 0D mode
    odometry_std_yaw: 0.01

    # minimum particle spread in x and y [m]
    min_sample_std_xy: 0.025

    # minimum particle spread in yaw angle [rad]
    min_sample_std_yaw: 0.025

    # initial/maximum particle spread in x and y [m]
    max_sample_std_xy: 0.5

    # initial/maximum particle spread in yaw angle [rad]
    max_sample_std_yaw: 0.5

    # threshold for 1D / 2D position decision making (minimum average second order gradient)
    #   if worst gradient direction is below this value we go into 1D mode
    #   if both gradient directions are below we may go into 0D mode, depending on disable_threshold
    #   higher values will make it go into 1D / 0D mode earlier
    constrain_threshold: 0.1

    # threshold for 1D / 2D decision making (with or without orientation)
    #   higher values will make it go into 1D mode earlier
    constrain_threshold_yaw: 0.2

    # minimum number of points per update
    min_points: 20

    # solver update gain, lower gain = more stability / slower convergence
    solver_gain: 0.1

    # solver update damping, higher damping = more stability / slower convergence
    solver_damping: 1000.0

    # number of gauss-newton iterations per sample per scan
    solver_iterations: 20

    # maximum wait for getting transforms [s]
    transform_timeout: 0.2

    # if to broadcast map frame
    broadcast_tf: true
    # Scan topic
    scan_topic: scan
    # Initial Pose topic
    initialpose: initialpose
    # Map Tile topic
    map_tile: map_tile
    # Map Pose topic
    map_pose: map_pose
    # particle_cloud topic
    particle_cloud: particlecloud
    # amcl_pose topic
    amcl_pose: amcl_pose
    # for debugging
    broadcast_info: false

    set_initial_pose: true
    initial_pose.x: 0.0
    initial_pose.y: 0.0
    initial_pose.yaw: 0.0
```

## Configuration
Please visit the [neobotix configuration page](https://neobotix-docs.de/ros/packages/neo_localization.html) to know more about the configuration.

## Compatibility
This package has been built and tested with the following Nav2 branches:

- [Nav2 Rolling branch](https://github.com/ros-navigation/navigation2) (main branch)
- [Nav2 Kilted branch](https://github.com/ros-navigation/navigation2/tree/kilted) (kilted branch)
