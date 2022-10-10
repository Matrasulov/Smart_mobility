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

```
parallels@ubuntu-linux-22-04-desktop:~/ros2_ws$ . install/setup.bash
```


