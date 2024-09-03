### `nav2_new_features`

#### Notes

1. Nav2 Simple Commander

```
sudo apt update
sudo apt install ros-galactic-nav2-simple-commander
```

2. Code [origin](https://github.com/ros-navigation/navigation2/tree/main/nav2_simple_commander/nav2_simple_commander)  

Specifically, in [`robot_navigator.py`](https://github.com/ros-navigation/navigation2/blob/main/nav2_simple_commander/nav2_simple_commander/robot_navigator.py)  

3. (Action) Navigate to pose

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

4. (Action) Navigate through poses

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

5. Waypoint following

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
