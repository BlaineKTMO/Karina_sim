# Simulation

## How-to

### Models

#### Karina 2D
The following command will launch the Karina 2D model in a Gazebo environment and RVIZ and also have a map .

`roslaunch aasha_description gazebo_2d.launch world:=map1`

You can change map1 to map2,map4,map4,etc.

##### Plugins
|  Type  | Plugin Name  | Description  |
| :------------ | :------------ | :------------ |
| 2D Camera  |  camera_controller | The 2D camera publishes live images at a specified rate from the simulated robot in Gazebo |
| 2D LIDAR  | gazebo_ros_head_hoyuko_controller  | The 2D LIDAR publishes laser scan data from the simulated robot in Gazebo which can be viewed in RVIZ |
| GPS Sim  | gazebo_ros_gps  |   |
| Defferential Drive Controller  | gazebo_libgazebo_ros_diff_drive  |   |
| Bird's Eye | Bird's Eye | |

#### Aasha 3D
The following command will launch the Aasha 3D model in a Gazebo environment and RVIZ.

`roslaunch karina_description gazebo_3d.launch`


##### Plugins
|  Type  | Plugin Name  | Description  |
| :------------ | :------------ | :------------ |
| 3D LIDAR | | |
| Stereo Camera | | |

## Universal Robot Description Format (URDF) File
The URDF file is a series of nested XML-like tags that describe the simulated robot's properties, constraints, physical attributes, and sensors to ROS. Below are some of the high-level tags and their purpose.

| Tag  | Description  |
| :------------ | :------------ |
| `<robot>`  | The root element in which all other tags are nested  |
|  <nbsp> `<link>`  <br>...<br>`</link>` | Link elements describe rigid bodies with appearances and physical properties, e.g., wheels, the robot’s frame, shapes representing sensors, etc.  |
| `<joint>`  <br>...<br>`</joint>`  | Joint elements describe where and how links are connected in terms of a parent link and a child link, e.g., wheels (child link) and the robot’s frame (parent link)  |
| `<gazebo>`  <br>...<br>`</gazebo>`  | Gazebo tags describe simulation extensions, such as cameras, LIDAR, and GPS  |
| `</robot>`  | Nothing can reside outside of the robot root element tags  |

Nested within these basic tags are more tags describing various properties of their parent tag. More information about what is typically found within some tags can be found on the [ROS Wiki](http://wiki.ros.org/ "ROS Wiki"), including in-depth descriptions of [link](http://wiki.ros.org/urdf/XML/link "link") elements and [joint](http://wiki.ros.org/urdf/XML/joint "joint") elements.

## Software

### Gazebo
![Gazebo](images/gazebo.png)
##### About
Gazebo is a simulation tool to mimic the real world. It can be used to simulate realistic conditions, such as indoor and outdoor environments, objects, surfaces, lights, and gravity. The robot itself and its sensors can also be simulated in Gazebo, and the robot can interact with the environment within these simulated conditions. Gazebo can be run in conjunction with RVIZ to gather useful data and test algorithms (such as lane following or object detection) in a safe, convenient, and cost-effective way.

##### Application
When running the simulation launch file, the simulated robot’s sensors create nodes and published messages that are defined in the URDF file. Additionally, the robot’s differential drive controller subscribes to the commonly used /cmd_vel topic. Running simulations in Gazebo is as simple as having your algorithms subscribe to the appropriate sensor topics and publish to the /cmd_vel topic.

### RQT
![RQT](images/rqt.png)
##### About
RQT is an interface which hosts plugins for interacting with or visualizing ROS information.  These plugins can be arranged on a dashboard to create a unique view and toolset for ROS and the robot. 

##### Application
Some common RQT plugins utilized by the simulation team are described below.

| Plugin  | Description  |
| :------------ | :------------ |
| Visualization <br>&#124;<br> Image View  | Image View is used to visualize all kinds of image data from the robot. The visualization is constantly updated, typically with image data from the robot within Gazebo.  |
| Introspection <br>&#124;<br> Node Graph  |  Node Graph displays all active and inactive ROS nodes and topics as well as their connections to each other. This tool can assist with understanding what nodes are publishing or subscribing to various ROS topics. |
| Robot Tools <br>&#124;<br> Robot Steering  | Robot steering provides a GUI to control the simulated robot’s forward/backward velocity in m/s and angular velocity in rad/s  |

### ROS Visualization (RVIZ)
![RVIZ](images/rviz.png)
##### About
RVIZ is a software used to visualize the robot’s perception of its environment, either in the real-world or simulated by Gazebo. Unlike Gazebo, RVIZ does not simulate an environment or real-world constraints. Instead, RVIZ provides a host of tools to visualize data such as images from the robot’s cameras, LIDAR detection, and point clouds.

##### Application
RVIZ can be used to visualize output from sensors defined in the URDF file when the simulation is actively running in Gazebo. For example, in the screenshot above, the robot’s 2D camera output is visible in the bottom left corner. This information can be helpful when developing and debugging algorithms.
