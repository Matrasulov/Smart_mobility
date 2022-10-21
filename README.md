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

# Publisher and Subscriber

## Prerequirements
the directory needs to be navigated to the **ros2_wc** directory

## Task
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ ros2 pkg create --build-type ament_python py_pubsub
going to create a new package
package name: py_pubsub
```
## Write the publishe rnode

Navigate into ros2_ws/src/py_pubsub/py_pubsub. Recall that this directory is a Python package with the same name as the ROS 2 package it’s nested in.

### Python package should be like this:
```
import rclpy
from rclpy.node import Node

from std_msgs.msg import String


class MinimalPublisher(Node):

    def __init__(self):
        super().__init__('minimal_publisher')
        self.publisher_ = self.create_publisher(String, 'topic', 10)
        timer_period = 0.5  # seconds
        self.timer = self.create_timer(timer_period, self.timer_callback)
        self.i = 0

    def timer_callback(self):
        msg = String()
        msg.data = 'Hello World: %d' % self.i
        self.publisher_.publish(msg)
        self.get_logger().info('Publishing: "%s"' % msg.data)
        self.i += 1


def main(args=None):
    rclpy.init(args=args)

    minimal_publisher = MinimalPublisher()

    rclpy.spin(minimal_publisher)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_publisher.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

## 2.1 Examine the code

The first lines of code after the comments import rclpy so its Node class can be used.

```
import rclpy
from rclpy.node import Node
```
The next statement imports the built-in string message type that the node uses to structure the data that it passes on the topic.

```
from std_msgs.msg import String
```
These lines represent the node’s dependencies. Recall that dependencies have to be added to package.xml, which you’ll do in the next section.

Next, the MinimalPublisher class is created, which inherits from (or is a subclass of) Node.

```
class MinimalPublisher(Node):
```
Following is the definition of the class’s constructor. super().__init__ calls the Node class’s constructor and gives it your node name, in this case minimal_publisher.

create_publisher declares that the node publishes messages of type String (imported from the std_msgs.msg module), over a topic named topic, and that the “queue size” is 10. Queue size is a required QoS (quality of service) setting that limits the amount of queued messages if a subscriber is not receiving them fast enough.

Next, a timer is created with a callback to execute every 0.5 seconds. self.i is a counter used in the callback.

```def __init__(self):
    super().__init__('minimal_publisher')
    self.publisher_ = self.create_publisher(String, 'topic', 10)
    timer_period = 0.5  # seconds
    self.timer = self.create_timer(timer_period, self.timer_callback)
    self.i = 0

timer_callback creates a message with the counter value appended, and publishes it to the console with get_logger().info.

def timer_callback(self):
    msg = String()
    msg.data = 'Hello World: %d' % self.i
    self.publisher_.publish(msg)
    self.get_logger().info('Publishing: "%s"' % msg.data)
    self.i += 1
```
Lastly, the main function is defined.

```
def main(args=None):
    rclpy.init(args=args)

    minimal_publisher = MinimalPublisher()

    rclpy.spin(minimal_publisher)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_publisher.destroy_node()
    rclpy.shutdown()
 ```

First the rclpy library is initialized, then the node is created, and then it “spins” the node so its callbacks are called.


### Adding  dependencies

***ros2_ws/src/py_pubsub*** directory needs to be  naviagated, where the ***setup.py***, ***setup.cfg***, and ***package.xml***vfiles have been created.



#### Open ***package.xml*** with your text editor.
```
<?xml version="1.0"?>
<?xml-model href="http://download.ros.org/schema/package_format3.xsd" schematypens="http://www.w3.org/2001/XMLSchema"?>
<package format="3">
  <name>py_pubsub</name>
  <version>0.0.0</version>
  <description>TODO: Package description</description>
  <maintainer email="akbarjon3524@gmail.com">parallels</maintainer>
  <license>TODO: License declaration</license>

  <test_depend>ament_copyright</test_depend>
  <test_depend>ament_flake8</test_depend>
  <test_depend>ament_pep257</test_depend>
  <test_depend>python3-pytest</test_depend>

  <export>
    <build_type>ament_python</build_type>
  </export>
</package>
```

## Adding entry point

Next step is to open ***setup.py*** file and and match the **maintainer**, **maintainer_email** variables.
```
zip_safe=True,
    maintainer='Akbarjon',
    maintainer_email='akbarjon3524@gmail.com',
```
    
    
## Checking setup.cfg
```
[develop]
script_dir=$base/lib/py_pubsub
[install]
install_scripts=$base/lib/py_pubsub
```

## Writing the subscriber node
 ***ros2_ws/src/py_pubsub/py_pubsub*** should be navigated.

```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src/py_pubsub/py_pubsub$ wget https://raw.githubusercontent.com/ros2/examples/humble/rclpy/topics/minimal_subscriber/examples_rclpy_minimal_subscriber/subscriber_member_function.py
.
.
subscriber_membe 100%[=========>]   1.43K  --.-KB/s    in 0s      

2022-10-11 11:11:58 (26.5 MB/s) - ‘subscriber_member_function.py’ saved [1469/1469]
 
 ```

Now the directory should have these files:

```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src/py_pubsub/py_pubsub$ ls
__init__.py                   subscriber_member_function.py
publisher_member_function.py
```

### Add an entry point

Reopen setup.py and add the entry point for the subscriber node below the publisher’s entry point. The entry_points field should now look like this:
```
entry_points={
        'console_scripts': [
                'talker = py_pubsub.publisher_member_function:main',
                'listener = py_pubsub.subscriber_member_function:main',
        ],
},
```
  ## Build and run
  
  Checking wheter packages are installed or not
  ```
  parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src/py_pubsub/py_pubsub$ sudo apt install python3-rosedep2
[sudo] password for parallels: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
E: Unable to locate package python3-rosedep2
```


```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src/py_pubsub/py_pubsub$ colcon build --packages-select py_pubsub
[0.196s] WARNING:colcon.colcon_core.package_selection:ignoring unknown package 'py_pubsub' in --packages-select
                     
Summary: 0 packages finished [0.10s]
```
###### Open a new terminal, navigate to ros2_ws, and source the setup files:

```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src/py_pubsub/py_pubsub$ cd 
parallels@ubuntu-linux-22-04-desktop:~$ cd ros2_ws
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ 
```

```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ . install/setup.bash
```

### Now run the talker node
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ ros2 run py_pubsub talker
[INFO] [1665470419.289797166] [minimal_publisher]: Publishing: "Hello World: 0"
[INFO] [1665470419.778375637] [minimal_publisher]: Publishing: "Hello World: 1"
[INFO] [1665470420.277981583] [minimal_publisher]: Publishing: "Hello World: 2"
```

[1665471515.777608986] [minimal_subscriber]: 
![image](https://user-images.githubusercontent.com/76453238/195022507-3be0b0f5-1cde-4cd8-940f-d573ea0a7229.png)

### Open another terminal, source the setup files from inside ros2_ws again, and then start the listener node:

```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ . install/setup.bash
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ ros2 run py_pubsub listener
[INFO] [1665471514.284184880] [minimal_subscriber]: I heard: "Hello World: 2190"
[INFO] [1665471514.777648718] [minimal_subscriber]: I heard: "Hello World: 2191"
[INFO] [1665471515.277583334] [minimal_subscriber]: I heard: "Hello World: 2192"
```
![image](https://user-images.githubusercontent.com/76453238/195023042-8413df15-fe7d-47c3-aeda-f297cf5e1881.png)


### Enter Ctrl+C in each terminal to stop the nodes from spinning
```
^CTraceback (most recent call last):
 .
 .
 .
KeyboardInterrupt
[ros2run]: Interrupt
```

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

## Wrting the service node
nside the ***ros2_ws/src/py_srvcli/py_srvcli*** directory, create a new file called **service_member_function.py** and paste the following code within:
```
GNU nano 6.2               service_member_function.py *                       

from example_interfaces.srv import AddTwoInts

import rclpy
from rclpy.node import Node


class MinimalService(Node):

    def __init__(self):
        super().__init__('minimal_service')
        self.srv = self.create_service(AddTwoInts, 'add_two_ints', self.add_two>

    def add_two_ints_callback(self, request, response):
        response.sum = request.a + request.b
        self.get_logger().info('Incoming request\na: %d b: %d' % (request.a, re>

        return response


def main(args=None):
    rclpy.init(args=args)

    minimal_service = MinimalService()

    rclpy.spin(minimal_service)

    rclpy.shutdown()


if __name__ == '__main__':
    main()

```


## Adiing entry point **setup.py** file
enrtry points of ***setup.py*** file should look like this:
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src/py_srvcli$ nano setup.py
entry_points={
    'console_scripts': [
        'service = py_srvcli.service_member_function:main',
        'client = py_srvcli.client_member_function:main',
    ],
},
```
don't forget to save it.


## Build and run
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ rosdep install -i --from-path src --rosdistro humble -y
#All required rosdeps installed successfully
```

Navigate back to the root of your workspace, ros2_ws, and build your new package:
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src/py_srvcli/py_srvcli$ colcon build --packages-select py_srvcli
[0.161s] WARNING:colcon.colcon_core.package_selection:ignoring unknown package 'py_srvcli' in --packages-select
                     
Summary: 0 packages finished [0.08s]
```
Open a new terminal, navigate to ros2_ws, and source the setup files:
```
. install/setup.bash
parallels@ubuntu-linux-22-04-desktop:~$ cd ros2_ws
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ . install/setup.bash
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ source /opt/ros/humble/setup.bash
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ ros2 run py_srvcli service
Package 'py_srvcli' not found
```

Open another terminal and source the setup files from inside ros2_ws again. Start the client node, followed by any two integers separated by a space:
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ cd src/py_srvcli/py_srvcli
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src/py_srvcli/py_srvcli$ ros2 run py_srvcli client 2 3
Package 'py_srvcli' not found
```
  
# Creating an action 
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ cd
parallels@ubuntu-linux-22-04-desktop:~$ source /opt/ros/humble/setup.bash
parallels@ubuntu-linux-22-04-desktop:~$ mkdir -p ros2_ws/src
parallels@ubuntu-linux-22-04-desktop:~$ cd ros2_ws/src
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ ros2 pkg create action_tutorials_interfaces
going to create a new package
package name: action_tutorials_interfaces
destination directory: /home/parallels/ros2_ws/src
package format: 3
version: 0.0.0
description: TODO: Package description
maintainer: ['parallels <akbarjon3524@gmail.com>']
```
<img width="736" alt="Screen Shot 2022-10-21 at 2 03 59 PM" src="https://user-images.githubusercontent.com/76453238/197116280-7a22458a-9aba-414e-84bf-ae44b759c7a4.png">


### Create an action directory in our ROS 2 package action_tutorials_interfaces:
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ cd action_tutorials_interfaces
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src/action_tutorials_interfaces$ mkdir action
```

### Within the action directory, create a file called Fibonacci.action with the following contents:
```
int32 order
---
int32[] sequence
---
int32[] partial_sequence
```


```
arallels@ubuntu-linux-22-04-desktop:~$ cd ros2_ws
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ colcon build
Starting >>> py_srvcli
--- stderr: py_srvcli                   
package init file 'py_srvcli/__init__.py' not found (or not a regular file)
/usr/lib/python3/dist-packages/setuptools/command/install.py:34: SetuptoolsDeprecationWarning: setup.py install is deprecated. Use build and pip and other standards-based tools.
  warnings.warn(
error: can't copy 'resource/py_srvcli': doesn't exist or not a regular file
---
Failed   <<< py_srvcli [0.55s, exited with code 1]

Summary: 0 packages finished [0.73s]
  1 package failed: py_srvcli
  1 package had stderr output: py_srvcli
```
<img width="715" alt="Screen Shot 2022-10-21 at 2 10 41 PM" src="https://user-images.githubusercontent.com/76453238/197117008-9e9d4d32-9b74-41ca-90a4-080a6dc32161.png">

# Writing an action server and client
```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ cd src
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ nano fibonacci_action_server.py
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ python3 fibonacci_action_server.py
Traceback (most recent call last):
  File "/home/parallels/ros2_ws/src/fibonacci_action_server.py", line 1, in <module>
    import rclpy
ModuleNotFoundError: No module named 'rclpy'
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ python3
Python 3.10.4 (main, Jun 29 2022, 12:14:53) [GCC 11.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import rclpy
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'rclpy'
>>> 
[1]+  Stopped                 python3
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ source 
action_tutorials_interfaces/ py_srvcli/
examples/                    ros2_ws/
fibonacci_action_server.py   setup.py
package.xml                  tutorial_interfaces/
py_pubsub/                   
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ source source /opt/ros/humble/setup.bash
bash: source: No such file or directory
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ python3 fibonacci_action_server.py
Traceback (most recent call last):
  File "/home/parallels/ros2_ws/src/fibonacci_action_server.py", line 1, in <module>
    import rclpy
ModuleNotFoundError: No module named 'rclpy'
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ source /
bin/        home/       mnt/        run/        swap.img    var/
boot/       lib/        opt/        sbin/       sys/        
dev/        lost+found/ proc/       snap/       tmp/        
etc/        media/      root/       srv/        usr/        
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ source /
bin/        home/       mnt/        run/        swap.img    var/
boot/       lib/        opt/        sbin/       sys/        
dev/        lost+found/ proc/       snap/       tmp/        
etc/        media/      root/       srv/        usr/        
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ source /opt/ros/humble/setup.bash
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ python3 fibonacci_action_server.py
Traceback (most recent call last):
  File "/home/parallels/ros2_ws/src/fibonacci_action_server.py", line 5, in <module>
    from action_tutorials_interfaces.action import Fibonacci
ImportError: cannot import name 'Fibonacci' from 'action_tutorials_interfaces.action' (unknown location)
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ python3 fibonacci_action_server.py
Traceback (most recent call last):
  File "/home/parallels/ros2_ws/src/fibonacci_action_server.py", line 5, in <module>
    from action_tutorials_interfaces.action import Fibonacci
ImportError: cannot import name 'Fibonacci' from 'action_tutorials_interfaces.action' (unknown location)
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ python3 fibonacci_action_server.py
Traceback (most recent call last):
  File "/home/parallels/ros2_ws/src/fibonacci_action_server.py", line 5, in <module>
    from action_tutorials_interfaces.action import Fibonacci
ImportError: cannot import name 'Fibonacci' from 'action_tutorials_interfaces.action' (unknown location)
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws/src$ 
```
