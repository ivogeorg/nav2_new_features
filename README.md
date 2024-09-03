### `nav2_new_features`

#### Notes

##### 1. Initial position

1. From the command line
```
ros2 topic pub /initialpose geometry_msgs/msg/PoseWithCovarianceStamped "{header: {stamp: {sec: 0}, frame_id: 'map'}, pose: {pose: {position: {x: 3.45, y: 2.15, z: 0.0}, orientation: {z: 1.0, w: 0.0}}}}"
```  

2. Notes
   1. `pub --once` is not enough!
   2. The publication should be terminated once the initial pose takes (and any goal is set) because it wreaks havoc on the localization and, thus, the mappings.  

##### 2. Nav2 Simple Commander

```
sudo apt update
sudo apt install ros-galactic-nav2-simple-commander
```

1. Code [origin](https://github.com/ros-navigation/navigation2/tree/main/nav2_simple_commander/nav2_simple_commander)  

Specifically, in [`robot_navigator.py`](https://github.com/ros-navigation/navigation2/blob/main/nav2_simple_commander/nav2_simple_commander/robot_navigator.py)  

2. (Action) Navigate to pose

_Definition (`NavigateToPose.action`):_  
```
#goal definition
geometry_msgs/PoseStamped pose
string behavior_tree
---
#result definition
std_msgs/Empty result
---
# feedback definition
geometry_msgs/PoseStamped current_pose
builtin_interfaces/Duration navigation_time
builtin_interfaces/Duration estimated_time_remaining
int16 number_of_recoveries
float32 distance_remaining
```

_Nodes:_  
```
user:~$ ros2 action info /navigate_to_pose
Action: /navigate_to_pose
Action clients: 1
    /bt_navigator
Action servers: 1
    /bt_navigator
```

3. (Action) Navigate through poses

_Definition (`NavigateThroughPoses.action`):_  
```
#goal definition
geometry_msgs/PoseStamped[] poses
string behavior_tree
---
#result definition
std_msgs/Empty result
---
#feedback definition
geometry_msgs/PoseStamped current_pose
builtin_interfaces/Duration navigation_time
builtin_interfaces/Duration estimated_time_remaining
int16 number_of_recoveries
float32 distance_remaining
int16 number_of_poses_remaining
```  

_Nodes:_  
```
user:~$ ros2 action info /navigate_through_poses
Action: /navigate_through_poses
Action clients: 0
Action servers: 1
    /bt_navigator
```  

4. Waypoint following

_Documentation:_ [Waypoint Follower](https://docs.nav2.org/configuration/packages/configuring-waypoint-follower.html)  

_Definition (`FollowWaypoints.action`):_  
```
#goal definition
geometry_msgs/PoseStamped[] poses
---
#result definition
int32[] missed_waypoints
---
#feedback definition
uint32 current_waypoint
```

_Nodes:_  
```
user:~$ ros2 action info /follow_waypoints
Action: /follow_waypoints
Action clients: 0
Action servers: 1
    /waypoint_follower
```  

##### 3. Costmap Filters

1. Keepout filters

Narrative is poor. See [notebook](assets/Nav2-New-Features-Advanced-ROS2-Navigation-The-Construct.pdf)  

2. Speed limits

**Notes:**
1. Seems like keepout-zone filters and speed-limit filters are mutually exclusive. At least this is what the materials imply, but of course that is not reliable.

2. Drawing rectangles with different hues of gray in _Preview on Mac OS_ results in invalid cells for speed filters, obviously some _out-of-range_ error.  
