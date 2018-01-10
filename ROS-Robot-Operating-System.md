# ROS - Robot Operating System


* __roscore__

    * Starts ros. I had to install it first with the command __sudo apt install python-roscore__

* __rostopic list__

    * Lists all the available rostopics. Also had to install first wc __sudo apt install python rostopic__
    * It has listed two
        * __/rosout__ ROS client libraries are required to publish console logging messages to the /rosout topic as a standard interface. 
        * __/rosout_agg__ is an aggregated feed for subscribing to console logging messages. This aggregated topic is offered as a performance improvement: instead of connecting to individual ROS nodes to receive their console messages, the aggregated message feed can instead be received directly from the rosout node. 

* __Installation__

    * All the above installations are installing the linux version of ROS. Linux has its own set of packages and they are from them. To install more packeges I have to follow a set of instructions to install the whole thing with the packeges that ros updates.

* __Arduiono as a node__

    * __sudo apt install ros-kinetic-rosserial-python ros-kinetic-rosserial-arduino__ will install rosserial on my computer that allows communication between ros and the arduino IDE
    * __rosrun rosserial_arduino make_libraries.py <sketchbook location>__ will set up ros.lib and the IDE will be able to recognise examples as well as communicate with ros.

* __std_msgs__ it has different type of variables defined in them that we can use fe.: UInt16 or string etc.

* __rostopic pub <topic name> <topic type> [data]__ allows us to publish to a topic a certain type of data.

* __rosparam__ rosparam is a command-line tool for getting, setting, and deleting parameters from the ROS Parameter Server

    * Commands:
	rosparam set	set parameter
	rosparam get	get parameter
	rosparam load	load parameters from file
	rosparam dump	dump parameters to file
	rosparam delete	delete parameter
	rosparam list	list parameter names
    * set robot_description -t models/robot-arm.urdf
        uses the html file that I have in robot-arm.urdf
* __rosrun robot_state_publisher robot_state_publisher__ launches the robot state publisher
* **rosrun joint_state_publisher joint_state_publisher _use_gui:
=true** launches the robot joint state publisher

[Lab journal](https://github.com/Csaba1988/roco222/blob/master/lab-journal.md)
