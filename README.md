# Crestron-Hubitat-Integration

The Crestron-Hubitat integration is a suite of Crestron modules that provide 
a way to integrate off-the-shelf Zigbee, Z-Wave, and IoT devices into a 
Crestron automation system using a Hubitat Elevation hub.  The Crestron 
modules interface with devices connected to the Hubitat hub through the 
Maker API app on the Hubitat.  The following types of devices are supported:

•	Buttons
•	Contact Sensors
•	Dimmers
•	Fan Controllers
•	Garage Door Controllers
•	Humidity Sensors
•	Light Sensors
•	Locks
•	Moisture Sensors
•	Motion Detectors
•	Phillips Hue Bulbs (White Ambiance and Color)
•	Presence Sensors
•	RGB and RGBW Bulbs
•	Shades
•	Switches / Outlets
•	Temperature Sensors
•	Thermostats

This module suite is released as shareware.  It is free for a developer to 
use on their own personal Crestron system or for a dealer to use in their 
showroom demo system.  However, if it is used on customer systems where a 
dealer will profit from it than I ask for a single payment of $100 from the 
dealer.  

What you get is 

1) My thanks
2) Permission for the dealer to use the module on as many client projects 
as they want
3) A copy of the Simpl# source code for the module (only a binary executable 
is included with the example program)
4) Good Karma

Payment can be made over Paypal to jay.m.basen@gmail.com

Thanks

A Crestron demo program is provided with modules to support all the above 
hardware.  Full S# source code is also provided.

A full article on the module suite can be found in Residential Tech Today 
Magazine can be found here: Coming Soon!

The following are the steps to install the system.  I use a switch, as an 
example, in the steps below, but it could be any of the above device types 
that can be integrated with a Hubitat Elevation Hub.

1.	First make sure that both the Crestron processor and the Hubitat 
Elevation hub have either static IP addresses or DHCP reservations so 
their IP addresses won’t change over time.  This is necessary for messages 
to reliably pass back and forth between the two systems.

2.	Assuming you have already registered your Hubitat Elevation Hub, 
connect to the IP address of the Hubitat hub using a browser and login 
using your username and password.

3.	Following the manufactures directions, place your Z-Wave, or Zigbee, 
switch into acquire mode.

4.	In your browser select “Devices” from the Hubitat menu and then click 
on the “Discover Devices” button. 

5.	Next click on either the “Z-Wave” or “Zigbee” button depending on the 
type of switch you are working with.

6.	Once the device is discovered you can enter a name for the switch and 
click on the “Save” button.

7.	Next click on “Apps” from the Hubitat menu.

8.	Click on the “Add Built-In App” button and select “Maker API” from the 
list of built in apps.

9.	In the Maker API configuration screen and click on “Select Devices” to 
display a list of devices that are connected to your Hubitat hub.  Then 
check the check box next to the switch you earlier connected to the Hubitat 
and click the “Update” button.  This is very important.  You must click the 
update button or the device will look like it is selected but it will NOT 
work properly with the Maker API app.

10.	Next scroll down to the bottom of the Maker API configuration screen.  
There you will see a series of http commands.  Each command begins with: 
http://<IP Address of Hubitat hub>/apps/api/XX where XX is the ID of the 
Maker App.  Save this number for later.  Also notice that each command 
includes access_token=xxxx-xxxx-xxxx-xxxx-xxxx.  Save the access token 
for later.

11.	Next right mouse button click on the “Get All Devices” link and select 
to open the link in a new browser tab.  In the new browser tab you will see 
the json returned by the Hubitat hub.  This json includes data for all the 
devices attached to your hub.  Find the entry for the switch you just added 
and copy down the “id” number of the switch.  If you have a number of 
devices connected to your hub you may find it easier to read the json if you 
use one of the many json formatters on the internet

12.	Finally, go back to the browser tab with the Hubitat hub user interface 
and press the “Done” button to close the Maker API app configuration page.

13.	Next using whatever procedure you are comfortable with, copy the .usp 
and .ush files from the Hubitat Demo.zip file to your Crestron Usrsplus 
directory.  Each of the .usp files has a # INCLUDEPATH statement that 
defines where the Hubitat.clz file will be located.  You need to change 
the include path to the location where this file will be located on your 
own computer.  I have experienced compile issues when the .clz file is placed 
in the Crestron Usrsplus directory so unfortunately this editing step is 
necessary.  After editing each .usp file you then just need to recompile 
them.  Don’t forget to copy the hubitat.clz file to the directory you 
specified in the INCLUDEPATH.

14.	After you have studied the code in the Hubitat Demo program you just 
need to
a.	Insert a “Hubitat Comm Manager” module into your own program.
b.	Fill the parameter fields on the Comm Manager module in with
i.	The IP address of the Hubitat Hub
ii.	The IP address of the Crestron Processor
iii.	The communications port you specified in step 7
iv.	The access token you copied down in step 10
v.	The Maker API app ID you copied down in step 10
c.	Insert a “Hubitat Switch” module into your program and fill in the 
Device ID parameter field with the switch’s device ID that you copied 
down in step 11.
d.	Now connect the various signals on the two modules in the same way 
you see them connected in the demo program
e.	You are done

There are also Crestron modules to support the ability to have IFTTT 
applets trigger a Crestron program or provide numerical data to a Crestron 
program.  This complements the IFTTT module on this Github and removes the 
necessity of adding a port forward on a home’s router to route IFTTT 
webhook messages to the Crestron processor.  Instead they are routed through 
the Hubitat cloud, to the Hubitat hub, and finally to the Crestron processor.  

