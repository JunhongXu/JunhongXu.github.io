---
layout: post
title: Building an automated navigating turtlebot using tensorflow with Jetson TX1 and iCreate 2
---

I am intersted in automated robots. It is my ultimate goal to build a robot 
that can help people do repetitive works like doing laundry or 
opening doors. In this project, I used tensorflow to train a convolutional neural network to make a 
Jetson TX1 powered robot navigate in a building hallway. 

<object type="application/x-shockwave-flash" style="width:450px; height:366px;" data="//www.youtube.com/v/BvOjQcOTBvU?color2=FBE9EC&amp;version=3">
        <param name="movie" value="//www.youtube.com/v/BvOjQcOTBvU?color2=FBE9EC&amp;version=3" />
        <param name="allowFullScreen" value="true" />
        <param name="allowscriptaccess" value="always" />
        </object>



I made a autonomous RC car during my 
undergraduate thesis using an iPhone and macbook pro 
(<a href="https://www.youtube.com/watch?v=n-B2iz8JORU">videos</a>).
I received a Jetson TX1 in early March. I decided to use this powerful 
embedded board to build an autonomous robot.  With this board, I am able to build a 
more powerful robot.

### Hardware list:

<ul>
    <li>
        <a href="http://store.irobot.com/default/create-programmable-programmable-robot-irobot-create-2/RC65099.html?cgid=us&gclid=Cj0KCQjwg7HPBRDUARIsAMeR_0j6nVglDxbb_psQgpGZF8ASBC2MMLX7-9Yg2NPhrsK9UyBqVj-7J20aAtvdEALw_wcB">iRobot Create 2</a>: 
        the robot base, max linear speed: -0.5m/s to 0.5m/s, 
        max angular speed: -4.5rad/s to 4.5m/s
    </li>
    <li>
        <a href="http://www.nvidia.com/object/embedded-systems-dev-kits-modules.html">
            Nvidia Jetson TX1
        </a>: computation board used in this project. 
    </li>
    <li>
       <a href="https://www.stereolabs.com/">
       Zed Stereo Camera
       </a>: RGBD stereo camera. Using stereo images to estimate depth information.
    </li>
    <li>
        <a href="https://www.amazon.com/SainSmart-HC-SR04-Ranging-Detector-Distance/dp/B004U8TOE6">
        Ultrasonic sensors</a> * 2: measure the distance using ultrasonic wave. 
    </li>
     <li>
        <a href="https://store.arduino.cc/usa/arduino-uno-rev3">
        Arduino Board
        </a>: read depth measurements from ultrasonic sensors to TX1.
    </li>
    <li>
       <a href="https://www.amazon.com/gp/product/B00FE0OHKK/ref=as_li_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B00FE0OHKK&linkCode=as2&tag=jetsonhacks-20&linkId=LEGLHUR5BPT67TNF">
            Battery
       </a>, 
       <a href="https://www.amazon.com/gp/offer-listing/B0064SHG0Y/ref=dp_olp_0?ie=UTF8&condition=all">
            battery monitor
       </a>, and 
       <a href="https://www.amazon.com/gp/product/B00ND7J38C/ref=as_li_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B00ND7J38C&linkCode=as2&tag=jetsonhacks-20&linkId=LMCXZYGEVS7VPAXG">
            battery charger
       </a>
    </li>
    <li>
        <a href="https://www.amazon.com/dp/B00DQFGH80/ref=asc_df_B00DQFGH805228717/?tag=hyprod-20&creative=394997&creativeASIN=B00DQFGH80&linkCode=df0&hvadid=167151358503&hvpos=1o1&hvnetw=g&hvrand=5647704028981021705&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9016512&hvtargid=pla-281221827342">
            USB hub 
        </a>: to connect different sensors to TX1.
    </li>
    <li>
        A playstation 3 controller to teleoperate the robot.
    </li>
    <li>
        ABS platform, screws, and standoffs. 
    </li>
</ul>

### Software:

I used Robot Operating System to control the robot and tensorflow to build the neural networks. 
There are two installation parts: on TX1 and on host PC. They both need ROS, but they require different ROS packages.

<b>On TX1</b>

* Install ROS on Jetson TX1: I followed instructions from <a href="http://wiki.ros.org/action/show/kinetic/Installation/Ubuntu?action=show&redirect=kinetic%2FInstallation%2FUbuntuARM">ros website</a> to install ROS on TX1.
Because we do not want full installation on TX1, we need to use <code>sudo apt-get install ros-kinetic-ros-base</code>.
After installing ROS, create a worksapce in the home directory:
```
    mkdir -p ~/catkin_ws/src
    cd ~/catkin_ws
    catkin_make
    source devel/setup.bash
```
* ROS packages: `zed-ros-wrapper` for using ROS with ZED, `create_autonomy` 
for using ROS to communicate with robot base, `ros-ps3joy`  to control the robot using PS3 controller,
and `rosserial_python`, `rosserial_arduino` for communicating with Arduino. 

    * ZED: In order to let TX1 communicate with ZED, we need to first download 
    <a href="https://www.stereolabs.com/developers/">ZED SDK</a>.
    Then, we are able to install `zed-ros-wrapper` using command
    ```
    cd ~/catkin_ws/src
    git clone https://github.com/stereolabs/zed-ros-wrapper.git
    cd ..
    catkin_make
    source ./devel/setup.bash
    ```
    
    * Install `create_autonomy`: follow the steps in 
    <a href="https://github.com/AutonomyLab/create_autonomy">AutonomyLab repo</a>
    
    * Install Arduino dependencies `rosserial_python`, `rosserial_arduino`: follow the steps in 
    <a href="http://wiki.ros.org/rosserial_arduino/Tutorials/Arduino%20IDE%20Setup">ROS wiki</a>
    . Replace `indigo` with `kinetic`
    
    * Install `ps3joy`: follow the steps on this <a href="http://wiki.ros.org/ps3joy">site</a>


* Install tensorflow on Jetson TX1: fortunately, JetsonHacks offered a pre-built python wheel file
for installing tensorflow on Jetson TX1. I followed their 
<a href="https://github.com/jetsonhacks/installTensorFlowJetsonTX">repo</a> and successfully built tensorflow on TX1.  

<b>On host PC</b>
* ROS to initialize roscore and visualize using rviz.
* tensorflow to train the model.

### Up and running

Before running ros on host and tx1, make sure `ROS_IP` and `ROS_MASTER_URI` are set correctly in `.bashrc` file.
`ROS_IP` should be device's IP address. `ROS_MASTER_URI` should be `http://HOST_IP:11311`.

On host PC, run 

```
roscore
```

On TX1, run these commands to build the package.
```
cd ~/catkin_ws/src
git clone https://github.com/JunhongXu/tx1-neural-navigation.git
cd ..
catkin_make
source devel/setup.bash
```

Run `roslaunch robot run_robot.launch` to launch the robot. 

Run `rosrun ps3joy ps3joy.py --countinuous` to connect PS3 controller with TX1 and off you go!

### Thoughts
In this project, I want to reduce human labelling in DAgger. Doing this in real-world is not travail because we can not 
rely on sensor measurements. By using recording policy to prevent the navigation policy 
overfitting sensor actions turns out to be effective. 
However, generalization to other environments is still a big problem.


### References:

https://github.com/stereolabs/zed-ros-wrapper

https://github.com/AutonomyLab/create_autonomy

http://www.jetsonhacks.com/