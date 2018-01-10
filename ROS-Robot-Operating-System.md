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

```
<?xml version="1.0"?>
<robot name="robot-arm">
  <link name="base_link">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/base.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="1.57 0 0" xyz="0 0 0" />
    </visual>
  </link>

  <link name="arm_base">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/arm_base.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="1.57 0 0" xyz="-0.05 -0.045 -0.062" />
    </visual>
  </link>

  <joint name="base to armbase" type="revolute">
    <axis xyz="0 0 1" />
    <limit effort="1000" lower="-3.14"
		upper="3.14" velocity="0.5" />
    <parent link="base_link"/>
    <child link="arm_base"/>
    <origin xyz="0 0 0.057" />
  </joint>

  <link name="upper_arm">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/upper_arm.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="1.57 0 0" xyz="-0.005 0.001 0.021"/>
    </visual>
  </link>

  <joint name="armbase to upperarm" type="revolute">
    <axis xyz="0 1 0" />
    <limit effort="1000" lower="1.57"
		upper="-1.57" velocity="0.5" />
    <parent link="arm_base"/>
    <child link="upper_arm"/>
    <origin xyz="0 0 0.047" />
  </joint>

  <link name="lower_arm">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/lower_arm.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="1.57 0 0" xyz="-0.00495 0.002 -0.1375"/>
    </visual>
  </link>

  <joint name="upperarm to lowerarm" type="revolute">
    <axis xyz="0 1 0" />
    <limit effort="1000" lower="-1.57"
		upper="1.57" velocity="0.5" />
    <parent link="upper_arm"/>
    <child link="lower_arm"/>
    <origin xyz="-0.00005 0 0.1585" />
  </joint>

  <link name="Gripper_baseplate">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/Gripper_baseplate.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="0 -1.57 3.14" xyz="-0.005 -0.0189 0.0483"/>
    </visual>
  </link>

  <joint name="lowerarm to gripperbase" type="revolute">
    <axis xyz="0 1 0" />
    <limit effort="1000" lower="-0.7"
		upper="0.7" velocity="0.5" />
    <parent link="lower_arm"/>
    <child link="Gripper_baseplate"/>
    <origin xyz="-0.0004 0 0.1581" />
  </joint>

  <link name="Gripper_Gear_arm_1">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/Gripper_Gear_arm_1.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="0 -1.57 3.14" xyz="-0.0044 0 0.02"/>
    </visual>
  </link>

  <joint name="gripperbase to grippergear" type="revolute">
    <axis xyz="1 0 0" />
    <limit effort="1000" lower="-1"
		upper="0.3" velocity="0.5" />
    <parent link="Gripper_baseplate"/>
    <child link="Gripper_Gear_arm_1"/>
    <origin xyz="0 -0.0189 0.0283" />
  </joint>

  <link name="Gripper_Short_arm_1">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/Gripper_Short_arm_1.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="3.14 1.57 0" xyz="0.0176 -0.0016 0.002"/>
    </visual>
  </link>

  <joint name="gripperbase to grippershortarm" type="revolute">
    <axis xyz="1 0 0" />
    <limit effort="1000" lower="-1.4"
		upper="0.7" velocity="0.5" />
    <mimic joint="gripperbase to grippergear" multiplier="1.25" offset="0.12"/>
    <parent link="Gripper_baseplate"/>
    <child link="Gripper_Short_arm_1"/>
    <origin xyz="0 -0.0173 0.0503" />
  </joint>

  <link name="gripper1">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/gripper1.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="0 -1.57 3.14" xyz="-0.0043 0.0257 0.0053"/>
    </visual>
  </link>

  <joint name="grippergear to gripper1" type="revolute">
    <axis xyz="1 0 0" />
    <limit effort="1000" lower="-1.4"
		upper="0.7" velocity="0.5" />
    <mimic joint="gripperbase to grippergear" multiplier="-1" offset="-0.35"/>
    <parent link="Gripper_Gear_arm_1"/>
    <child link="gripper1"/>
    <origin xyz="0 -0.0276 0.0007" />
  </joint>

  <link name="Gripper_Gear_arm_2">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/Gripper_Gear_arm_2.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="0 -1.57 3.14" xyz="0.0367 -0.0191 0.0199"/>
    </visual>
  </link>

  <joint name="gripperbase to grippergear2" type="revolute">
    <axis xyz="1 0 0" />
    <limit effort="1000" lower="-1.4"
		upper="0.7" velocity="0.5" />
    <mimic joint="gripperbase to grippergear" multiplier="-1" offset="0.06"/>
    <parent link="Gripper_baseplate"/>
    <child link="Gripper_Gear_arm_2"/>
    <origin xyz="0 0.0002 0.0285" />
  </joint>

  <link name="gripper2">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/gripper2.stl" scale="0.001 0.001 0.001"/>
      </geometry>
      <origin rpy="0 -1.57 0" xyz="0.0299 -0.0257 0.0053"/>
     </visual>
  </link>

  <joint name="grippergear2 to gripper2" type="revolute">
    <axis xyz="1 0 0" />
    <limit effort="1000" lower="-1.4"
		upper="0.7" velocity="0.5" />
    <mimic joint="gripperbase to grippergear" multiplier="1" offset="0.29"/>
    <parent link="Gripper_Gear_arm_2"/>
    <child link="gripper2"/>
    <origin xyz="0 0.0277 0.0013" />
  </joint>

</robot>


```
<?xml version="1.0"?>
<robot name="robot-arm">
  <link name="base_link">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/base.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="1.57 0 0" xyz="0 0 0" />
    </visual>
  </link>

  <link name="arm_base">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/arm_base.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="1.57 0 0" xyz="-0.05 -0.045 -0.062" />
    </visual>
  </link>

  <joint name="base to armbase" type="revolute">
    <axis xyz="0 0 1" />
    <limit effort="1000" lower="-3.14"
		upper="3.14" velocity="0.5" />
    <parent link="base_link"/>
    <child link="arm_base"/>
    <origin xyz="0 0 0.057" />
  </joint>

  <link name="upper_arm">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/upper_arm.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="1.57 0 0" xyz="-0.005 0.001 0.021"/>
    </visual>
  </link>

  <joint name="armbase to upperarm" type="revolute">
    <axis xyz="0 1 0" />
    <limit effort="1000" lower="1.57"
		upper="-1.57" velocity="0.5" />
    <parent link="arm_base"/>
    <child link="upper_arm"/>
    <origin xyz="0 0 0.047" />
  </joint>

  <link name="lower_arm">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/lower_arm.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="1.57 0 0" xyz="-0.00495 0.002 -0.1375"/>
    </visual>
  </link>

  <joint name="upperarm to lowerarm" type="revolute">
    <axis xyz="0 1 0" />
    <limit effort="1000" lower="-1.57"
		upper="1.57" velocity="0.5" />
    <parent link="upper_arm"/>
    <child link="lower_arm"/>
    <origin xyz="-0.00005 0 0.1585" />
  </joint>

  <link name="Gripper_baseplate">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/Gripper_baseplate.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="0 -1.57 3.14" xyz="-0.005 -0.0189 0.0483"/>
    </visual>
  </link>

  <joint name="lowerarm to gripperbase" type="revolute">
    <axis xyz="0 1 0" />
    <limit effort="1000" lower="-0.7"
		upper="0.7" velocity="0.5" />
    <parent link="lower_arm"/>
    <child link="Gripper_baseplate"/>
    <origin xyz="-0.0004 0 0.1581" />
  </joint>

  <link name="Gripper_Gear_arm_1">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/Gripper_Gear_arm_1.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="0 -1.57 3.14" xyz="-0.0044 0 0.02"/>
    </visual>
  </link>

  <joint name="gripperbase to grippergear" type="revolute">
    <axis xyz="1 0 0" />
    <limit effort="1000" lower="-1"
		upper="0.3" velocity="0.5" />
    <parent link="Gripper_baseplate"/>
    <child link="Gripper_Gear_arm_1"/>
    <origin xyz="0 -0.0189 0.0283" />
  </joint>

  <link name="Gripper_Short_arm_1">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/Gripper_Short_arm_1.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="3.14 1.57 0" xyz="0.0176 -0.0016 0.002"/>
    </visual>
  </link>

  <joint name="gripperbase to grippershortarm" type="revolute">
    <axis xyz="1 0 0" />
    <limit effort="1000" lower="-1.4"
		upper="0.7" velocity="0.5" />
    <mimic joint="gripperbase to grippergear" multiplier="1.25" offset="0.12"/>
    <parent link="Gripper_baseplate"/>
    <child link="Gripper_Short_arm_1"/>
    <origin xyz="0 -0.0173 0.0503" />
  </joint>

  <link name="gripper1">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/gripper1.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="0 -1.57 3.14" xyz="-0.0043 0.0257 0.0053"/>
    </visual>
  </link>

  <joint name="grippergear to gripper1" type="revolute">
    <axis xyz="1 0 0" />
    <limit effort="1000" lower="-1.4"
		upper="0.7" velocity="0.5" />
    <mimic joint="gripperbase to grippergear" multiplier="-1" offset="-0.35"/>
    <parent link="Gripper_Gear_arm_1"/>
    <child link="gripper1"/>
    <origin xyz="0 -0.0276 0.0007" />
  </joint>

  <link name="Gripper_Gear_arm_2">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/Gripper_Gear_arm_2.stl" scale="0.001 0.001 0.001" />
      </geometry>
      <origin rpy="0 -1.57 3.14" xyz="0.0367 -0.0191 0.0199"/>
    </visual>
  </link>

  <joint name="gripperbase to grippergear2" type="revolute">
    <axis xyz="1 0 0" />
    <limit effort="1000" lower="-1.4"
		upper="0.7" velocity="0.5" />
    <mimic joint="gripperbase to grippergear" multiplier="-1" offset="0.06"/>
    <parent link="Gripper_baseplate"/>
    <child link="Gripper_Gear_arm_2"/>
    <origin xyz="0 0.0002 0.0285" />
  </joint>

  <link name="gripper2">
    <visual>
      <geometry>
	<mesh filename="file:///home/csaba/Documents/roco222/robot-project/robot-arm/gripper2.stl" scale="0.001 0.001 0.001"/>
      </geometry>
      <origin rpy="0 -1.57 0" xyz="0.0299 -0.0257 0.0053"/>
     </visual>
  </link>

  <joint name="grippergear2 to gripper2" type="revolute">
    <axis xyz="1 0 0" />
    <limit effort="1000" lower="-1.4"
		upper="0.7" velocity="0.5" />
    <mimic joint="gripperbase to grippergear" multiplier="1" offset="0.29"/>
    <parent link="Gripper_Gear_arm_2"/>
    <child link="gripper2"/>
    <origin xyz="0 0.0277 0.0013" />
  </joint>

</robot>

```

![RVIZrep](https://github.com/Csaba1988/roco222/blob/master/DC_motor_images/RVIZrep.png)

* __Arduino code to control servo__

```

#include<ros.h>
#include<std_msgs/UInt16.h>
#include<Servo.h>

using namespace ros;


NodeHandle  nh;
Servo servo;

void cb(const std_msgs ::UInt16& msg){
  servo.write(msg.data);// 0-180
}
Subscriber<std_msgs::UInt16> sub("servo", cb);

void setup(){

  nh.initNode();
  
  nh.subscribe(sub);
  
  servo.attach(9);//attach it to pin 9
}

void loop(){

nh.spinOnce();

delay(1);
}

```

    * The function cd takes a type UInt16 from std_msg and servo.write(msg.data); writes that data to  
the servo hence moving it.



[Lab journal](https://github.com/Csaba1988/roco222/blob/master/lab-journal.md)
