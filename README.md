# Turtlesim installation

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





