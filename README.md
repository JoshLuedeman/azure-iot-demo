# My IOT Demo

## Summary
This is a simple demo that I put together. This application will run on a Raspberry PI and stream temperature data to an Azure IoTHub.

## Requirements

* An Azure Subscription
* A Raspberry Pi Device
* A DS18B20 temperature sensor for a Raspberry Pi device

## Configuring your Raspberry Pi

1. Follow the diagram in the image below to connect the DS18B20 temperature sensor.

![Wiring Diagram](http://www.circuitbasics.com/wp-content/uploads/2016/03/Raspberry-Pi-DS18B20-1024x450.png)

2. Configure your Raspberry Pi so that it can connect to your sensor via the GPIO interface. This has to be enabled at boot. Add the following code to your boot config located at `/boot/config.txt`. To do this you will need to use sudo to utilize superuser priviledges to make edits to the file. At the command prompt enter `sudo nano /boot/config.txt`. When prompted for your password, enter it at the prompt.
3. Scroll through the entire file and at the end add the following code: `dtoverlay=w1-gpio`
4. Exit Nano and save the file, then reboot the Raspberry Pi.
5. When the Raspberry Pi finishes rebooting, we need to get the Pi to connect to the new sensor. At a command prompt enter `sudo modprobe w1-gpio`. Then enter `sudo modprobe w1-therm`.
6. Now that we have initialized the new device, lets make sure its showing as connected and sending data.
7. Change directories `cd /sys/bus/w1/devices`. Once in the directory, type `ls` to list the connected devices.
8. Change directory to the device. The device directory will start with "28-" and then followed by many digits.
9. To read the current value from the sensor, type `cat w1_slave`. You should see the value that is returned look similar to the image below. 

![Device Output](http://www.circuitbasics.com/wp-content/uploads/2016/03/Raspberry-Pi-DS18B20-Temperature-Sensor-Tutorial-DS18B20-Raw-Output.png)

The `t=` is the temperature value. For instance, in the example above, `t=28625` is equal to a temperature of 28.625 degrees Celcius.

10. Enter `cd` to return to the root directory.
11. Upload the temp.py file from this repository to the Raspberry Pi.
