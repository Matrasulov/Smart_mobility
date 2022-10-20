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
