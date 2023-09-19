# Overview
This project is developed to enable velocity control using Radio Controller (RC) in offboard mode while using the ARPL Autonomy stack. The ROS-RC-Wrapper is a ROS Package that maps the RCin topics from Mavros to Body Velocity commands in the ARPL Quadrotor control.
# Subscribers and Services
This package mainly subscribes to Mavros and calls multiple services from the Mav_manager package. The following is a list Subscribers and Services used by the package. 

| Object Type | Topic Name    | Description | 
|-------------|--------------|------|
| Subscriber  | /mavros/rc/in | Stick input from the RC streamed via Mavros |
| Subscriber  | /mavros/param/get | PX4 parameters set in the PX4 firmware |
| Service     | /mav_services/setDesVelInBodyFrame | Desired Velocity goals in Body frame |
| Service     | /mav_services/land | Land service |
| Service     | /mav_services/hover | Hover service | 
| Service     | /mav_services/motors | Motors-on Service |
| Service     | /mav_services/takeoff | Takeoff Service |

# Installation
The installation of the package is straight forward. Make sure to source `setup.bash` before begining installation of the package.

```
cd ~/path/to/your/workspace/src
git clone https://github.com/arplaboratory/ROS-RC-Wrapper.git
catkin build rc_control
source ~/path/to/your/workspace/devel/setup.bash 
```
# Running
You can run the package using `rosrun` in the following way

```
rosrun rc_control rc_command
```
# Usage
To send body velocity goals using the RC follow these steps,

## Set up
1. Once the ARPL Autonomy Stack is running you can start the ROS-RC-Wrapper package using `rosrun`
2. Follow the regular procedure until motors-on in the RVIZ interface.

## Takeoff
1. After motors-on is clicked, toggle `SWITCH F` on the RC to `POS 1` to switch to "Offboard" mode.
2. Toggle `SWITCH D` to `POS 1` to takeoff.
> **Note:**
> At this point the robot will be flying and will be in offboard mode as usual.

## Velocity Control

1. Toggle `SWITCH F` to `POS 0` to enable velocity control. 
> **Important:**
> Make sure both the sticks are centered before toggling to Velocity mode to avoid publishing any unnecesary goals during transition.

## Landing
1. Toggle the `SWITCH F` back to `POS 1` to disable Velocity control.
2. Toggle `SWITCH D` to `POS 0` to land the robot. 

## Disarming 
1. To disarm the Robot, switch mode back to stabilize by toggling `SWITCH F` to `POS 2`
2. Then disarm by toggling the disarm switch `SWITCH A` to `POS 1`

> [!WARNING]
> Make sure the **THROTTLE STICK** is set to **ZERO** before switching mode to stabilize. This is to avoid commanding high throttle during disarming.
