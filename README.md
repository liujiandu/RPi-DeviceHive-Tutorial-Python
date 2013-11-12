RPi-DeviceHive-Tutorial-Python
==============================

Tutorial that shows how to read from a temperature sensor and control a light using DeviceHive cloud platform

Tutorial is based on example located at http://www.devicehive.com/samples/python-and-raspberry-pi-temperature-sensor.

================
Assemble Circuit
================
======================
Configure Raspberry Pi
======================
<ol>
<li>Load 1-wire kernel modules that come pre-installed but not loaded:</li>
<pre class="code-text-only" style="display: none;">
<code>sudo modprobe w1-gpio</code>
<code>sudo modprobe w1_therm</code>
</pre>
<li>Add lines w1-gpio and w1_therm into /etc/modules using sudo nano /etc/modules so they get loaded automatically next time you restart it.</li>
<li>Find your sensor: ls /sys/bus/w1/devices/ it should look like 28-00000393268a</li>
<li>Test the sensor, by printing out it’s output: cat /sys/bus/w1/devices/28-00000393268a/w1_slave</li>
</ol>
=====================================
Installing DeviceHive on Raspberry Pi
=====================================
<ol>
<li>Go to home/pi directory</li>
<li>Git the latest code from this repository</li>
<pre class="code-text-only" style="display: none;">
<code>git clone https://github.com/mvartani76/RPi-DeviceHive-Tutorial-Python</code>
</pre>
<li>Go to <b>devicehive.com/playground</b> and create yourself an account for a playground if you don’t have one.</li>
<li>On your RasPi edit ~/devicehive/examples/raspi_led_thermo.py and change _W1_FILENAME and _API_URL url (usually http://nnXXX.pg.devicehive.com/api if created using playground) to match the environment, using nano editor.</li>
<li>Install Twisted and DeviceHive device libraries. The DeviceHive python library is built using twisted engine. A very powerful tool to build protocol and connectivity libraries.</li>
<pre class="code-text-only" style="display: none;">
<code>sudo apt-get install python-twisted</code>
<code>~/devicehive run sudo python setup.py install</code>
</pre>
<li>Run the script:</li>
<pre class="code-text-only" style="display: none;">
<code>sudo python ~/devicehive/examples/raspi_led_thermo.py</code>
</pre>
</ol>
================================
Access your device from Admin UI
================================
<ol>
<li>After a first run of the script you can see the device and the readings from the sensor in Admin UI (http://nnXXX.pg.devicehive.com/admin, login as admin / your_playground_password). Go to Devices tab, and click “detail” for your device), then go to “notifications”.</li>
<li>You can also send on/off messages to the LED: go to “commands” for your device, click “enter new command”, set name as UpdateState and parameters as {"equipment":"LED","state":"1"}, then click “push”. The LED will turn on.
 Sending the parameters as {"equipment":"LED","state":"0"} will turn the LED off.</li>
</ol>
=================
Create Client App
=================
<ol>
<li>Login to the DeviceHive administrative console. Go to the Users tab and create new user of the Client role. Click on the Networks button for this user and grant access to the your device network.</li>
<li>Now, it’s time for the actual client app. Let’s use JavaScript. The client sample code to match your installation of playground. For example go to ~/examples/RasPiClient of the JavaScript repository.</li>
<li>Open index.html file. Find the line where new DeviceHive instance is created and insert your assigned DeviceHive service URL; login and password of the client user you created on step 1. As a result, it should look like the following:</li>
<pre class="code-text-only" style="display: none;">
<code>var deviceHive = new DeviceHive("http://yourinstance.pg.devicehive.com/api", "myclientuser", "mypassword");</code>
<code>app.start(deviceHive, "9f33566e-1f8f-11e2-8979-c42c030dd6a5");</code>
</pre>
The GUID specifies unique identifier of the device we will be interacting with, it does not have to be changed if you use sample devices from DeviceHive sources.
<li>Open index.html in your browser. The application should now work, displaying current LED state, and allowing you to switch on/off the LED and get temperature readings.</li>
</ol>

