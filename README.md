# ROS-commands<img height="40px" align="right" src="https://upload.wikimedia.org/wikipedia/commons/b/bb/Ros_logo.svg" alt=""/>

---
## Raspberry pi: <img height="40px" align="right" src="https://www.vectorlogo.zone/logos/raspberrypi/raspberrypi-icon.svg" alt=""/>                          

<details>
 <summary><ins>ROS installation on raspberry pi:</ins></summary>
 ✴ Need to install ubuntu 20.04 LTS, install server then you can upgrade to disktop if needed
<pre><code class="language-shell">sudo nano /etc/rc.local
</code></pre> 
✴ If you want delay
<pre><code class="language-shell">sleep 30
</code></pre> 
✴ Add this to the end:(example)
<pre><code class="language-shell">su -c "python3 /path/to/your/script.py > /path/to/your/logfile.log 2>&1" pi &
</code></pre> 
✴ if you want to run chrome in kiosk mode:(example)
<pre><code class="language-shell">su -c "/usr/bin/chromium-browser --kiosk --disable-session-crashed-bubble --disable-infobars http://localhost:5555" pi
</code></pre> 
✴ Update permission:
<pre><code class="language-shell">sudo chmod +x /etc/rc.local
</code></pre> 
</details>



