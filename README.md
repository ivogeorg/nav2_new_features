### `nav2_new_features`

#### Notes

1. Nav2 Simple Commander

```
sudo apt update
sudo apt install ros-galactic-nav2-simple-commander
```

2. (Action) Navigate to pose

_Definition:_  
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
