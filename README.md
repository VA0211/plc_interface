Where to change to run test:
- comm_check/unit_test.py
Line 48,49,63,64
- config/motor_config.yaml
- launch/plc_remote_control.launch

Maybe need to change to fit our need
- msg/encoder_data.msg
- scripts/plc_controller.py 
- odometry_caliberation/caliberation.py
---
This repository is developed to perform the following tasks:

1. Perform a sanity check that confirms coherency in the communication between the PLC and PC

2. Perform test on PLC and ROS communication by having PLC peripherals controlled by ROS teleop keyboard


Perfoming Basic Sanity check
----------------------------
This functionality checks the communication between the PC and the PLC by performing a series of read and write operations on each of the designated Memory registers on the PLC  (as configured for the project).
The module logs all the operations performed and provides a PASS/FAIL result for read/write operations performed on each register.

To run this module follow the instructions below :

1.  Go into the comm_check folder

    `cd ~/ws/src/plc_interface/comm_check`

2. Run the python script

    `python3 unit_tests.py`

Once the code completes execution, a log file named 'plc_init_checks.log' will be created in the **comm_check/scripts/** folder path which shall contain the result of the communication sanity check of the PC and PLC


ROS PLC Communication Check
---------------------------
This module is developed to perform tests on the ROS PLC communication interface. The module performs this check by having a ROS node communicate velocity commands provided by the ROS teleop keyboard by subscribing to the "/cmd_vel" topic. The node converts the velocities provided by the "/cmd_vel" topic to Motor RPM values and sends them to the PLC on the configured memory addesses.
The node also reads in Motor Encoder data and converts it into an odometry message and publishes onto the "/odom" topic.

The user has to provide velocity information through the teleop keyboard.

To use this module, follow the instructions provided below.

1. go to the ros_plc_interface directory

    `cd ~/ws`

2. build the ROS packages

    `colcon build --symlink-install`

3. source the ROS workspace

    `source install/setup.bash`

4. run the launch file

    `ros2 launch mw_mitsubishi_plc_interface remote_control.launch`

5. provide velocity commands from the keyboard

6. in another terminal instance/window/tab, to check the odometry data, run the following command

    `ros2 topic echo /odom`
