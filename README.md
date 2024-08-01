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




