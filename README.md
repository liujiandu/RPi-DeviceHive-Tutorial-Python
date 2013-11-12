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


