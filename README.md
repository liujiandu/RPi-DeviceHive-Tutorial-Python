RPi-DeviceHive-Tutorial-Python
==============================

Tutorial that shows how to read from a temperature sensor and control a light using DeviceHive cloud platform

Tutorial is based on example located at http://www.devicehive.com/samples/python-and-raspberry-pi-temperature-sensor.
<ol>
<li><b>Assemble Circuit</li>
<li><b>Install necessary libraries</b></li>
Load 1-wire kernel modules that come pre-installed but not loaded:
sudo modprobe w1-gpio and then sudo modprobe w1_therm
Add lines w1-gpio and w1_therm into /etc/modules using sudo nano /etc/modules so they get loaded automatically next time you restart it.
</ol>

