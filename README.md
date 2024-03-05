# ROS2 Foxy Project Introduction

Welcome to the ROS2 Foxy project focused on establishing publisher and subscriber nodes for converting Unix epoch time to human-readable time at regular intervals. This project serves as an introductory exercise for the SDSU Mechatronics Club, aiming to familiarize members with ROS2 development.

For more information about the SDSU Mechatronics Club, please visit [https://www.sdsumechatronics.org/](https://www.sdsumechatronics.org/).

## Setup

### Required OS

Ensure your system runs `Ubuntu LTS 20.04` to support this project. You can either set up a dual boot or create a virtual machine. If choosing the latter, download the Ubuntu Desktop ISO file from [here](https://releases.ubuntu.com/20.04.5/). Refer to this [link](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview) for detailed tutorials on setting up an Ubuntu virtual machine.

### Installing ROS2 Foxy

Follow the instructions provided on [docs.ros.org](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html) to install and set up ROS2 (Foxy).

## Project

Refer to the following basic [tutorials](https://docs.ros.org/en/foxy/Tutorials.html) for this project (Sections [Beginner: CLI Tools](https://docs.ros.org/en/foxy/Tutorials/Beginner-CLI-Tools.html) and [Beginner: Client Libraries](https://docs.ros.org/en/foxy/Tutorials/Beginner-Client-Libraries.html) would suffice for this project).

This project is primarily written in Python. You can find instructions for writing in C++ [here](https://docs.ros.org/en/foxy/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Cpp-Publisher-And-Subscriber.html).

You will reference this [page](https://docs.ros.org/en/foxy/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Py-Publisher-And-Subscriber.html) extensively during the project. It contains all necessary information for writing publishers and subscribers for ROS2 Foxy (Python).

## Overview

The project involves establishing a publisher node that updates and publishes Unix epoch time every 5 seconds. Subsequently, a subscriber node receives this information and converts it to human-readable time, displaying it in the terminal. This cycle continues until the program is terminated (using Ctrl+C).

### Publisher

The publisher node retrieves the current Unix epoch time and sends it to the subscriber node. The code is based on a free sample program, `MinimalSubscriber()`. You can install the file by executing the following command in the terminal:

```bash
wget https://raw.githubusercontent.com/ros2/examples/foxy/rclpy/topics/minimal_subscriber/examples_rclpy_minimal_subscriber/subscriber_member_function.py
```

### Subscriber

The subscriber node listens to a topic named `unix_epoch_time`, expecting messages of type `Int64`. Upon receiving a message, it converts the Unix epoch time to a human-readable date string of the format `YYYY-MM-DD HH:MM:SS`. The resulting string is then published to another topic called `human_readable_date` as a message of type `String`.

### Add Dependencies and Entry Points

Ensure you set up dependencies and entry points correctly to avoid build failures. Here's the format for entry points in `setup.py`:

```python
entry_points={
    'console_scripts': [
            '<publisher_name> = <package_name>.<publisher_file_name>:main',
            '<subscriber_name> = <package_name>.<subscriber_file_name>:main',
    ],
},
```

## Code (Execution)

1. Source the ROS2 environment:
   ```bash
   source /opt/ros/foxy/setup.bash
   ```

2. Build the workspace:
   ```bash
   colcon build --packages-select <package_name>
   ```

3. Open two new terminals, navigate to your workspace, and run:
   ```bash
   source install/setup.bash
   ```

4. In one terminal, execute:
   ```bash
   ros2 run py_pubsub unix_time_pub
   ```

5. In the other terminal, execute:
   ```bash
   ros2 run py_pubsub unix_time_sub
   ```

![unix_epoch_time.png](https://github.com/ayuyamo/ROS2-epoch-time-converter/blob/2f23a628a6dc41fe55418f7546baeba4d7f5962d/unix_epoch_time.png)




