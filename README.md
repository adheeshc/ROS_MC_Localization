# Turtlebot_EKF

<p align="center">
  <img src="/Images/world.gif" alt="obstacle">
</p>
  
## Overview  
In this lab, I will be applying an EKF ROS package to localize the Turtlebot robot inside a Gazebo environment. In the end, I will be able to drive the robot around in simulation and observe and compare the unfiltered `Odom` and filtered `EKF` trajectories.

## Prerequisites/Dependencies  
* Gazebo >= 7.0  
* ROS Kinetic  
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
## Setup Instructions (abbreviated)  
1. Meet the `Prerequisites/Dependencies`  
2. Open Ubuntu Bash and clone the project repository  
3. On the command line execute  
```bash
sudo apt-get update && sudo apt-get upgrade -y
```
4. Build and run your code.  

## Packages Used

- turtlebot_gazebo
- turtlebot_teleop
- robot_pose_ekf
- odom_to_trajectory

## Project Description  
Directory Structure  
```
Turtlebot_EKF                           # Turtlebot_EKF src directory contents
    ├── main                            # Main package that launches all other packages together
    ├── odom_to_trajectory              # [Odometry to Trajectory package](https://github.com/udacity/odom_to_trajectory)
    ├── robot_pose_ekf                  # [Robot Pose EKF package](http://wiki.ros.org/robot_pose_ekf)
    ├── turtlebot                       # [Turtlebot package](http://wiki.ros.org/turtlebot)
    ├── turtlebot_simulator             # [Turtlebot gazebo package](http://wiki.ros.org/turtlebot_gazebo)
    ├── EKFLab.rviz                     # RViz default settings file
    └── RvizLaunch.launch               # Rviz Launch file
```

## Run the project  

#### Step 1 Create a Catkin Workspace
```sh
$ mkdir -p /home/workspace/catkin_ws/src
$ cd /home/workspace/catkin_ws/src
$ catkin_init_workspace
$ cd ..
$ catkin_make
```

#### Step 2 Perform a System Update/Upgrade
```sh
$ apt-get update
$ apt-get upgrade -y
```

#### Step 3 Clone the Package in src
```sh
$ cd /home/workspace/catkin_ws/src
$ git clone https://github.com/adheeshc/Turtlebot_EKF
```

#### Step 4 Edit the main.launch file
Under main/launch, edit the main.launch file:
```html
Delete this: <node pkg="rviz" type="rviz" name="rviz" args="-d /home/workspace/catkin_ws/src/EKFLab.rviz"/>
Replace with: <node pkg="rviz" type="rviz" name="rviz" args="-d /home/<workspace>/catkin_ws/src/EKFLab.rviz"/>

where <workspace> is your workspace
```

#### Step 5 Install Packages Dependancies
```sh
$ cd /home/workspace/catkin_ws/
$ source devel/setup.bash
$ rosdep -i install turtlebot_gazebo
$ rosdep -i install turtlebot_teleop
$ apt-get install ros-kinetic-rqt -y
$ apt-get install ros-kinetic-rqt-multiplot -y
$ apt-get install libqwt-dev -y
$ rm -rf ~/.config/ros.org/rqt_gui.ini
```

#### Step 6 Build the Packages
```sh
$ catkin_make
$ source devel/setup.bash
```

#### Step 7 Launch the main file
```sh
$ roslaunch main main.launch
```
Now, you should see Gazebo and rviz launching. Please note that Gazebo might take up to 3 min to launch! 


### End Result
In the terminal, use the keyboard commands(u-i-o-j-k-l-m-,-.) and drive the robot around. The `red` trajectory represents the `Odom path` whereas the `green` trajectory represents the `EKF path`.