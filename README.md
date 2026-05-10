
# LiDAR-Based Mapping and Person Following Robot Using ROS

## Project Overview

This project focuses on using **LiDAR-based sensing**, **ROS robot control**, **SLAM mapping**, and **PID-based person following** for an autonomous mobile robot.

The project was completed as part of **ECE 600 Applied Robotics Lab** by Team Jupiter. The main objective was to understand how a mobile robot can use LiDAR data, odometry, teleoperation, SLAM, and feedback control to map an indoor environment and follow a person safely.

The project had two major parts:

1. **Mapping:** Using LiDAR and SLAM to create an occupancy grid map of an indoor environment.
2. **Person Following:** Using LiDAR tracking and PID tuning to allow the robot to follow a person while maintaining a safe distance.

---

## Objectives

- Bring up and control a mobile robot using ROS.
- Use LiDAR data to scan the surrounding environment.
- Run SLAM to create a real-time map.
- Use keyboard teleoperation to manually guide the robot during mapping.
- Save the generated occupancy grid map.
- Configure and tune PID parameters for person-following behavior.
- Enable autonomous person following with stable and safe robot motion.
- Validate the final behavior through testing and video demonstration.

---

## Tools and Technologies Used

- ROS
- TurtleBot / Yahboom Robot Platform
- LiDAR Sensor
- SLAM
- GMapping
- RViz
- Gazebo
- ROS Teleoperation
- `map_server`
- `rqt_reconfigure`
- PID Control
- Linux Terminal
- Occupancy Grid Mapping

---

## Methodology and Project Execution

The project was completed in two main phases: mapping and person following.

---

## Part A: Mapping

The first part of the project focused on creating a map of the indoor environment using LiDAR and SLAM.

### 1. Robot Bringup

The robot was first launched using the ROS bringup command. This initialized the robot system and prepared it for simulation and control.

```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
````

---

### 2. Launching SLAM

After bringing up the robot, SLAM was launched to allow the robot to build a map of the environment using LiDAR scan data.

```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch
```

SLAM allowed the robot to combine laser scans, odometry, and robot motion to build an occupancy grid map in real time.

---

### 3. Launching RViz

RViz was used to visualize the robot, LiDAR scans, and generated map.

```bash
roslaunch turtlebot3_gazebo turtlebot3_gazebo_rviz.launch
```

This helped monitor how the robot was mapping the room as it moved.

---

### 4. Teleoperation for Mapping

Keyboard teleoperation was used to manually drive the robot around the environment. This allowed the robot to scan different areas and complete the map.

```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

During this stage, the robot was controlled using keyboard commands for forward, backward, left rotation, right rotation, speed increase, and speed decrease.

The mapping process required careful driving because the robot was not controlled like a remote-control car. The movement was based on linear and angular velocity commands.

---

### 5. Saving the Map

After the environment was mapped, the map was saved using `map_server`.

```bash
rosrun map_server map_saver -f my_map
```

The map was saved as:

```text
my_map.pgm
my_map.yaml
```

These files represent the generated occupancy grid map and map metadata.

---

## Part B: Person Following

The second part of the project focused on autonomous person following using LiDAR-based tracking and PID control.

### 1. Robot Bringup

The robot was brought up again before starting the person-following system.

```bash
roslaunch <robot_bringup>
```

---

### 2. PID Controller Tuning

The person-following behavior required PID tuning to make the robot follow smoothly and safely.

PID control was used to adjust the robot’s motion based on the person’s position and distance. The goal was to prevent sudden movements, overshooting, oscillation, or unsafe following distance.

The parameters were adjusted using `rqt_reconfigure`.

Important parameters included:

| Parameter       | Purpose                                     |
| --------------- | ------------------------------------------- |
| `lin_Kp`        | Controls forward/backward response strength |
| `lin_Ki`        | Corrects accumulated linear distance error  |
| `lin_Kd`        | Reduces sudden linear speed changes         |
| `ang_Kp`        | Controls turning response strength          |
| `ang_Ki`        | Corrects accumulated angular error          |
| `ang_Kd`        | Smooths turning behavior                    |
| `laserAngle`    | Defines the LiDAR detection angle           |
| `ResponseDist`  | Sets safe following distance                |
| `priorityAngle` | Defines priority tracking angle             |
| `switch`        | Enables/disables person-following mode      |

The tuning process required trial and error. The PID values were adjusted until the robot followed the person smoothly without aggressive movement.

---

### 3. Final Autonomous Person Following

After the PID parameters were tuned, the tested values were loaded into the robot’s default configuration. This allowed the robot to follow a person autonomously.

The robot was able to:

* Detect a person using LiDAR-based tracking
* Maintain a safe distance
* Adjust speed based on distance
* Adjust direction based on person position
* Follow smoothly without excessive oscillation

A final video demonstration was recorded showing the autonomous person-following behavior.

---

## System Workflow

```text
Robot Bringup
        ↓
LiDAR Activation
        ↓
SLAM Launch
        ↓
RViz Visualization
        ↓
Keyboard Teleoperation
        ↓
Room Mapping
        ↓
Save Occupancy Grid Map
        ↓
Robot Bringup for Person Following
        ↓
PID Parameter Tuning
        ↓
Load Tested Parameters
        ↓
Autonomous Person Following
```

---

## Results and Outcomes

The project successfully demonstrated both mapping and person-following behavior.

Major outcomes included:

* Successfully launched the robot using ROS.
* Used LiDAR data for indoor environment sensing.
* Ran SLAM to build a live occupancy grid map.
* Controlled the robot using keyboard teleoperation during mapping.
* Saved the generated map as `my_map.pgm` and `my_map.yaml`.
* Tuned PID parameters for stable person following.
* Reduced unsafe motion by adjusting linear and angular control gains.
* Enabled autonomous person-following behavior.
* Validated the final result through video demonstration.

---

## Key Features

* LiDAR-based environment sensing
* SLAM-based mapping
* Real-time occupancy grid generation
* RViz visualization
* Keyboard teleoperation
* ROS map saving
* PID-based motion control
* Person-following behavior
* Safe-distance tracking
* Autonomous robot movement

---

## Commands Used

### Launch Robot World

```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

### Launch SLAM

```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch
```

### Launch RViz

```bash
roslaunch turtlebot3_gazebo turtlebot3_gazebo_rviz.launch
```

### Launch Teleoperation

```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

### Save Map

```bash
rosrun map_server map_saver -f my_map
```

### Open Dynamic Reconfigure

```bash
rosrun rqt_reconfigure rqt_reconfigure
```

---

## PID Tuning Summary

| Parameter       | Tuned Value / Purpose          |
| --------------- | ------------------------------ |
| `lin_Kp`        | Linear proportional response   |
| `lin_Ki`        | Linear integral correction     |
| `lin_Kd`        | Linear derivative smoothing    |
| `ang_Kp`        | Angular proportional response  |
| `ang_Ki`        | Angular integral correction    |
| `ang_Kd`        | Angular derivative smoothing   |
| `laserAngle`    | LiDAR tracking angle           |
| `ResponseDist`  | Safe following distance        |
| `priorityAngle` | Person tracking priority range |

PID tuning was one of the most important parts of the project because person following must be smooth, stable, and safe.

---

## Repository Structure

```text
.
├── README.md
├── Checkpoint 7.pdf
├── Autonomous Code.mp4
├── maps/
│   ├── my_map.pgm
│   └── my_map.yaml
├── launch/
│   └── robot_bringup.launch
└── docs/
    └── checkpoint_report.pdf
```

---

## Applications

This project is useful for understanding:

* Indoor mobile robot mapping
* Autonomous navigation foundations
* LiDAR-based tracking
* Human-following robots
* Service robotics
* Warehouse robots
* Assistive mobile robots
* ROS-based feedback control
* SLAM and localization workflows

---

## Major Learnings

Through this project, I gained practical experience with:

* ROS robot bringup
* LiDAR sensor usage
* SLAM and mapping
* Occupancy grid generation
* RViz visualization
* Keyboard teleoperation
* Map saving using `map_server`
* PID control tuning
* Person-following robot behavior
* Safe autonomous motion control
* Real-world robotics testing and debugging

---

## Conclusion

This project successfully demonstrated LiDAR-based mapping and autonomous person following using ROS.

In the mapping phase, the robot used LiDAR scans, odometry, and SLAM to generate and save a map of the indoor environment. In the person-following phase, PID control parameters were tuned so the robot could follow a person smoothly while maintaining a safe distance.

Overall, the project provided hands-on experience in mobile robotics, LiDAR sensing, SLAM, ROS control, PID tuning, and autonomous robot behavior.

```
```
