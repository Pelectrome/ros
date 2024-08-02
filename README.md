# ROS-commands<img height="40px" align="right" src="https://upload.wikimedia.org/wikipedia/commons/b/bb/Ros_logo.svg" alt=""/>

---
## Raspberry pi: <img height="40px" align="right" src="https://www.vectorlogo.zone/logos/raspberrypi/raspberrypi-icon.svg" alt=""/>                          

<details>
 <summary><ins>ROS installation on raspberry pi:</ins></summary>
 
✴ Need to install ubuntu 20.04 LTS, install server then you can upgrade to disktop if needed
 
✴ Setup your computer to accept software from packages.ros.org.
<pre><code class="language-shell">sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
</code></pre> 
 
✴ if you haven't already installed curl
<pre><code class="language-shell">sudo apt install curl
</code></pre> 
 
✴ Set up your keys
<pre><code class="language-shell">curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
</code></pre> 
 
✴ make sure your Debian package index is up-to-date:
<pre><code class="language-shell">sudo apt update
</code></pre> 
 
✴ Desktop-Full Install:
<pre><code class="language-shell">sudo apt install ros-noetic-desktop-full
</code></pre> 
 
✴ Environment setup
<pre><code class="language-shell">source /opt/ros/noetic/setup.bash
</code></pre> 
 
✴ automatically source this script every time a new shell is launched
<pre><code class="language-shell">echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
</code></pre>

✴ Dependencies for building packages:
<pre><code class="language-shell">sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
</code></pre>

✴ Initialize rosdep:
<pre><code class="language-shell">sudo apt install python3-rosdep
</code></pre>

✴ you can initialize rosdep:
<pre><code class="language-shell">sudo rosdep init
rosdep update
</code></pre>

</details>

<details>
 <summary><ins>To start ROS as master (server):</ins></summary>

✴ Set the ros host ip so can clients access to it in local network:
<pre><code class="language-shell">export ROS_HOSTNAME=MASTER_IP
</code></pre>

✴ in new terminal:
<pre><code class="language-shell">roscore
</code></pre> 

✴ to connect client to master in local network:
✴ in client side:
<pre><code class="language-shell">export ROS_MASTER_URI=http://MASTER_IP:11311
</code></pre> 
 
</details>

<details>
 <summary><ins>Create a ROS workspace:</ins></summary>

✴ Create the Workspace Directory:
<pre><code class="language-shell">mkdir -p ~/catkin_ws/src
</code></pre>

✴ Navigate to the Workspace Directory:
<pre><code class="language-shell">cd ~/catkin_ws/
</code></pre> 

✴ Initialize the Workspace:
<pre><code class="language-shell">catkin_make
</code></pre> 

✴ Source the Workspace:
<pre><code class="language-shell">source ~/catkin_ws/devel/setup.bash
</code></pre> 

</details>

<details>
 <summary><ins>Create ROS node:</ins></summary>

✴ Navigate to the src Directory of Your Workspace:
<pre><code class="language-shell">cd ~/catkin_ws/src
</code></pre>

✴ Create a New Package:
<pre><code class="language-shell">catkin_create_pkg counter_tutorial std_msgs rospy roscpp
</code></pre> 

✴ Build the Workspace:
<pre><code class="language-shell">cd ~/catkin_ws
catkin_make
</code></pre> 

✴ Create the Node:

✴ Navigate to the Package Directory:
<pre><code class="language-shell">cd ~/catkin_ws/src/counter_tutorial
</code></pre> 

✴ Create a scripts Directory:
<pre><code class="language-shell">mkdir scripts
</code></pre> 

✴ Create a Python Script:
<pre><code class="language-shell">nano scripts/counter.py
</code></pre> 

✴ Add the Following Code to counter.py:
<pre><code class="language-python">
#!/usr/bin/env python

import rospy
from std_msgs.msg import Int32

def counter():
    rospy.init_node('counter_node', anonymous=True)
    pub = rospy.Publisher('counter', Int32, queue_size=10)
    rate = rospy.Rate(1)  # 1 Hz

    count = 0
    while not rospy.is_shutdown():
        rospy.loginfo(count)
        pub.publish(count)
        count += 1
        rate.sleep()

if __name__ == '__main__':
    try:
        counter()
    except rospy.ROSInterruptException:
        pass

</code></pre> 

✴ Make the Script Executable:
<pre><code class="language-shell">chmod +x scripts/counter.py
</code></pre> 

✴ Modify the Package Configuration:
<pre><code class="language-shell">nano CMakeLists.txt
</code></pre> 

✴ Add the Following Line to the End of the CMakeLists.txt File:
<pre><code class="language-shell">
 catkin_install_python(PROGRAMS scripts/counter.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
</code></pre> 

✴ Build the Package:
<pre><code class="language-shell">
 cd ~/catkin_ws
 catkin_make
</code></pre> 

✴ Source the Workspace:
<pre><code class="language-shell">source devel/setup.bash
</code></pre> 

✴ Run the Node:
<pre><code class="language-shell">rosrun counter_tutorial counter.py
</code></pre> 

✴ In the Master side:

✴ rostopic list:
<pre><code class="language-shell">rostopic list
</code></pre> 

✴ Echo the Topic:
<pre><code class="language-shell">rostopic echo /counter
</code></pre> 
 
</details>

<details>
 <summary><ins>Open RViz:</ins></summary>
 
<pre><code class="language-shell">rviz
</code></pre>

<pre><code class="language-shell">rosrun rviz rviz
</code></pre>
 
</details>



