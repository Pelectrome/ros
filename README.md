# ROS-commands<img height="40px" align="right" src="https://upload.wikimedia.org/wikipedia/commons/b/bb/Ros_logo.svg" alt=""/>

---
## Raspberry pi: <img height="40px" align="right" src="https://www.vectorlogo.zone/logos/raspberrypi/raspberrypi-icon.svg" alt=""/>                          

<details>
 <summary><ins>Better way to run on startup script:</ins></summary>
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
 <details>
 <summary><ins>Run app with UI in startup use this:</ins></summary>
<pre><code class="language-shell">sudo nano /etc/xdg/lxsession/LXDE-pi/autostart
</code></pre> 
✴ Add this in the end:(example)
<pre><code class="language-shell">@/usr/bin/python /home/pi/example.py
</code></pre> 
</details>
 <details>
 <summary><ins>Hide the taskbar command this line:</ins></summary>
<pre><code class="language-shell">sudo nano /etc/xdg/lxsession/LXDE-pi/autostart
</code></pre> 
✴ Command this line:
<pre><code class="language-shell">#@lxpanel --profile LXDE-pi
</code></pre> 
</details>
 <details>
 <summary><ins>Chnage splash screen:</ins></summary>
  <div>✴ First change the splash image in what you like in this dir:
	<ul>/usr/share/plymouth/themes/pix</ul>
</div>
✴ Then run this command:
<pre><code class="language-shell">sudo plymouth-set-default-theme --rebuild-initrd pix
</code></pre> 
<div>✴ Disable rainbow splash:
	<ul>Add or edit this line:</ul>
</div>
<pre><code class="language-shell">disable_splash=1 to /boot/config.txt
</code></pre> 
✴ To remove the blinking curse add this:
<pre><code class="language-shell">vt.global_cursor_default=0 
</code></pre> 
✴ To:
<pre><code class="language-shell">/boot/cmdline.txt
</code></pre> 
✴ Mute kernel logs (only show critical errors) Add:
<pre><code class="language-shell">loglevel=3
</code></pre> 
✴ To:
<pre><code class="language-shell">/boot/cmdline.txt 
</code></pre> 
</details>
 <details>
 <summary><ins>Run GUI script from SSH:</ins></summary>
✴ Run this command:
<pre><code class="language-shell">export DISPLAY=:0
</code></pre> 
✴ Now you can run the script
</details>
 <details>
 <summary><ins>Run GUI script:</ins></summary>
✴ Add to python script:
<pre><code class="language-shell">os.environ["DISPLAY"] = ":0"
</code></pre> 
✴ Now you can run the script
</details>
<details>
 <summary><ins>Install picamera2:</ins></summary>
✴ Run this command:
<pre><code class="language-shell">sudo apt install -y python3-picamera2
</code></pre> 
</details>
<details>
 <summary><ins>Make raspberry discoverable by local network:</ins></summary>
✴ Run this command:
<pre><code class="language-shell">sudo nano /etc/avahi/avahi-daemon.conf
</code></pre> 
✴ In [server] section uncomment and modify this line to your desired hostname:
<pre><code class="language-shell">#host-name=foo
</code></pre>
✴ Run this command:
<pre><code class="language-shell">sudo service avahi-daemon restart
</code></pre>
✴ To discover it:
<pre><code class="language-shell">ping hostname.local
</code></pre> 
</details>
<details>
 <summary><ins>Set a static IP address for Raspberry Pi:</ins></summary>
✴ Run this command:
<pre><code class="language-shell">sudo nano /etc/dhcpcd.conf
</code></pre> 
✴ In end of the file add the following lines:
<pre><code class="language-shell">interface wlan0
static ip_address=192.168.1.100/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1
</code></pre>
✴ Run this command:
<pre><code class="language-shell">sudo service dhcpcd restart
</code></pre>
</details>
<details>
 <summary><ins>Permanently hide mouse pointer on Raspberry pi:</ins></summary>
✴ Run this command:
<pre><code class="language-shell">sudo nano /etc/lightdm/lightdm.conf
</code></pre> 
✴ Add this to the file after [Seat:*]:
<pre><code class="language-shell">xserver-command = X -nocursor
</code></pre> 
</details>
<details>
 <summary><ins>Bind flask to port 80:</ins></summary>
✴ Install authbind:
<pre><code class="language-shell">sudo apt install authbind
</code></pre> 
✴ Configure access to port 80:
<pre><code class="language-shell">sudo touch /etc/authbind/byport/80
sudo chmod 777 /etc/authbind/byport/80
</code></pre> 
✴ For security:
<pre><code class="language-shell">sudo chmod 550 /etc/authbind/byport/80
sudo chgrp {groupname} /etc/authbind/byport/80
sudo usermod -a -G {groupname} {username}
</code></pre> 
✴ To run:
<pre><code class="language-shell">authbind --deep python3 main.py
</code></pre> 
</details>
<details>
 <summary><ins>Create hotspot network on Raspberry pi:</ins></summary>
✴ Create hotspot for wifi_device:
<pre><code class="language-shell">sudo nmcli device wifi hotspot ssid {hotspot_name} password {hotspot_password} ifname {wifi_device}
</code></pre> 
✴ Example:
<pre><code class="language-shell">sudo nmcli device wifi hotspot ssid Home_5GHz password 12345678 ifname wlan0
</code></pre> 
✴ To get hotspot_UUID:
<pre><code class="language-shell">nmcli connection
</code></pre>
✴ Set autoconnect to hotspot:
<pre><code class="language-shell">sudo nmcli connection modify {hotspot_UUID} connection.autoconnect yes connection.autoconnect-priority 100
</code></pre> 
✴ To verify:
<pre><code class="language-shell">nmcli connection show {hotspot_UUID}
</code></pre> 
🚨 Important to let DNS working and internet sharing:
<pre><code class="language-shell">sudo nmcli connection modify {hotspot_UUID} ipv4.addresses 192.168.4.1/24 ipv4.method shared
</code></pre> 
</details>


