# Turtlesim installation
 This installation is for **Humble** version of ubuntu(latest version).
## Initially we update the system
```
parallels@ubuntu-linux-22-04-desktop:~$ sudo apt update
Hit:1 http://ports.ubuntu.com/ubuntu-ports jammy-security InRelease
Get:2 http://packages.ros.org/ros2/ubuntu jammy InRelease [4,673 B]
Hit:3 http://ports.ubuntu.com/ubuntu-ports jammy InRelease    

```

## Install the turtlesim package for your ROS 2 distro:
```
parallels@ubuntu-linux-22-04-desktop:~$ sudo apt install ros-humble-turtlesim
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
```

## Installing the turtlesim library(Humble version)
```
parallels@ubuntu-linux-22-04-desktop:~$ sudo apt install ros-humble-turtlesim
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libdouble-conversion3 libmd4c0 libpcre2-16-0 libqt5core5a
  libqt5dbus5 libqt5gui5 libqt5network5 libqt5svg5
  libqt5widgets5 libxcb-xinerama0 libxcb-xinput0
  qt5-gtk-platformtheme qttranslations5-l10n
...
```
## We check wheter library is installed or not
```
parallels@ubuntu-linux-22-04-desktop:~$ ros2 pkg executables turtlesim
turtlesim draw_square
turtlesim mimic
turtlesim turtle_teleop_key
turtlesim turtlesim_node
```

### if it shows:
```
parallels@ubuntu-linux-22-04-desktop:~$ ros2 pkg executables turtlesim
ros2: command not found

```
### we need to source our terminal, then it represents wheter library is checked or not.
```
parallels@ubuntu-linux-22-04-desktop:~$ source / opt/ros/humble/setup.bash
bash: source: /: is a directory
```

## To start turtlesim, following command in trhe terminal needs to be entered:
```
parallels@ubuntu-linux-22-04-desktop:~$ ros2 run turtlesim turtlesim_node
Warning: Ignoring XDG_SESSION_TYPE=wayland on Gnome. Use QT_QPA_PLATFORM=wayland to run on Wayland anyway.
[INFO] [1663735476.420497242] [turtlesim]: Starting turtlesim with node name /turtlesim
[INFO] [1663735476.424786260] [turtlesim]: Spawning turtle [turtle1] at x=[5.544445], y=[5.544445], theta=[0.000000]
```
## The simulator window should appear, with a random turtle in the center.
```
```
![This is an image](<img width="280" alt="image" src="https://user-images.githubusercontent.com/76453238/193712441-2f571dbc-63d3-44ef-95d9-aa3d66ca6531.png">)



## Following command needs to entered to control the turtle
```
parallels@ubuntu-linux-22-04-desktop:~$ ros2 run turtlesim turtle_teleop_key
Reading from keyboard
---------------------------
Use arrow keys to move the turtle.
Use G|B|V|C|D|E|R|T keys to rotate to absolute orientations. 'F' to cancel a rotation.
'Q' to quit.
```

# RQT  installation
```
parallels@ubuntu-linux-22-04-desktop:~$ sudo apt install ~nros-humble-rqt*
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  blt fonts-lyx gdal-data ibverbs-providers libaacs0 libaec0
  libaom3 libarmadillo10 libarpack2 libavcodec-dev
```


## We need source beforehand
```
parallels@ubuntu-linux-22-04-desktop:~$ source /opt/ros/humble/setup.sh
```

## Run RQT
```
parallels@ubuntu-linux-22-04-desktop:~$ rqt
libGL error: pci id for fd 42: 1ab8:0010, driver (null)
pci id for fd 43: 1ab8:0010, driver (null)
Service "/turtle1/set_pen" is no longer available. Refresh the list of services
Service "/turtle1/set_pen" is no longer available. Refresh the list of services
Service "/turtle1/set_pen" is no longer available. Refresh the list of services
```


# Installing colcon
```
parallels@ubuntu-linux-22-04-desktop:~$ sudo apt install python3-colon-common-extensions
[sudo] password for parallels: 
Reading package lists... Done
```

```
parallels@ubuntu-linux-22-04-desktop:~$ mkdir -p ~/ros2_ws/src
```

```
parallels@ubuntu-linux-22-04-desktop:~$ cd ~ros2_ws
```


## Add some sources
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ git clone https://github.com/ros2/examples src/examples -b humble
Cloning into 'src/examples'...
remote: Enumerating objects: 6690, done.
remote: Counting objects: 100% (1569/1569), done.
remote: Compressing objects: 100% (446/446), done.
```


## Build the workspace
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ colcon build --symlink-install
Starting >>> examples_rclcpp_async_client
Starting >>> examples_rclcpp_cbg_executor
```
## After the build is finished, we should see the build, install, and log directories:

```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ ls
build  install  log  src
.
├── build
├── install
├── log
└── src

4 directories, 0 files
```

## Running test
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ colcon test
Starting >>> examples_rclcpp_async_client
[0.500s] ERROR:colcon.colcon_cmake.task.cmake.test:Failed to find the following files:
- /home/parallels/ros2_ws/install/examples_rclcpp_async_client/share/examples_rclcpp_async_client/package.sh
Check that the following packages have been built:
- examples_rclcpp_async_client
```
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ . install/setup.bash
```




## Try a demo

With the environment sourced we can run executables built by colcon. Let’s run a subscriber node from the examples:

```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ ros2 run examples_rclcpp_minimal_subscriber subscriber_member_function
```
In another terminal, let’s run a publisher node (don’t forget to source the setup script):

```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ ros2 run examples_rclcpp_minimal_publisher publisher_member_function
```
