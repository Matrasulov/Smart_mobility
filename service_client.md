# Writing a simple service and client (Python)

## Tasks

## Creating a package

###### Open a new terminal and source your ROS 2 installation so that ros2 commands will work.

###### Navigate into the ros2_ws directory created in a previous tutorial.

###### Recall that packages should be created in the src directory, not the root of the workspace. Navigate into ros2_ws/src and create a new package:
```
parallels@ubuntu-linux-22-04-desktop:~$ source /opt/ros/humble/setup.bash
parallels@ubuntu-linux-22-04-desktop:~$ cd ros2_ws
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ cd src/
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ ros2 pkg create --build-type ament_python py_srvcli --dependencies rclpy example_interfaces
going to create a new package
package name: py_srvcli
destination directory: /home/parallels/ros2_ws/src
package format: 3
version: 0.0.0
```

## Update package.xml file
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ nano package.xml
<description>Python client server tutorial</description>
<maintainer email="you@email.com">Your Name</maintainer>
<license>Apache License 2.0</license>
```

## Updating setup.py file
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src/py_srvcli$ ls
package.xml  py_srvcli  resource  setup.cfg  setup.py  test
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src/py_srvcli$ nano setup.py
maintainer='Your Name',
maintainer_email='you@email.com',
description='Python client server tutorial',
license='Apache License 2.0',
```
