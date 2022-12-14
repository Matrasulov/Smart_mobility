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
