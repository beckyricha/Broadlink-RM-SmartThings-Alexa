# Read the main [readme](https://github.com/beckyricha/Broadlink-RM-LAN-Control/blob/master/README.md) for this repository first!
This document contains the setup instructions for the SmartApp version that does not require a SmartThings hub, instead using cloud-based control and the app "RM Bridge" as a bridge.  Thie requires that you open a port on your router.  You should, at a minimum, set up the security features in the RM Bridge app, but may wish to consider other security concepts as well.  Research and decisions about network security are your responsibility, and I won't be liable for that if you use this code.

## Set up your network
Obtain an externally accessible and stable ip address.  This will be easiest if you use a dynamic DNS service, whihc can be ontained for free.  Setting that up is outside the scope of this readme but caan be found online easily.

Forward the proper port on your router to the android device you will be using as a bridge.  The RM bridge app defaults to port 7474 but you can use whatever port you want.  Again, instructions vary by router and you will need to find that online if you don;t already know how.

## Set-up your Broadlink RM:
I used the app designed for this device by its manufacturer (e-Control, available in the play store) to set it up and add devices. I also installed it on the same android where the RM tasker is running, as it seemed to most reliably import the codes this way.  I only use this app as a bridge to this setup but it can be installed and run on multiple devices if you also want to control things using the app directly.  It's not bad on its own.  My Broadlink arrived with a manual only in Chinese, but install the e-Control app and follow its instructions to add your broadlink RM device to your wifi network. Don’t worry -the app is in English.  I did not take detailed notes during this section and mine is already set up, but it was like many other apps.  You can also add devices in the Broadlink e-Control app as you wish (for instance if you also want to use that app for device control), but that does not affect anything in the RM Bridge app or in SmartThings.  

## Set up your Android bridge:
Install the RM Bridge app, change any of hte settings you wish and press the red circle where it says "stopped" to start it. Note the ip address and port where the bridge is operating, as well as your user name and password if you are using them.  It will be most reliable if you can set your android up with a static ip address, but that is beyond the scope of this tutorial (it can vary for different android devices but is usually accessible under wifi settings by long pressing the name of your wifi network and selecting the advanced options).  

## Add some devices to control:
For this to work, you need to record devices directly using a web portal that is designed for setting up devices with the "RM Bridge" app.  You might want to read through this whole section before trying one, as both the concept and the steps are important.  To make devices work with this app, you need to set them up in a very specific way.  
We are going to add devices here and assign them functions that happen when you turn them on and when you turn them off in smartthings. This doesn't need to actually be the power button on your remote.  Let's walk through the steps, and then I will explain some creative ways to use them afterward.  

1. Go to http://rm-bridge.fun2code.de/rm_manage/index.html
2. Click the "manage codes" button with the wrench icon
3. Click "create new codes"
4. Enter the local IP address and port that the RM bridge app shows when you start it up, and click "load devices." (note - if you added security in the RM Bridge settings, you will need to enter your user name and password when prompted.  Alternately you can just enter your ip adress as username:password@xxx.xx.xxx:xxxx where the x's are your ip address and port from the RM Bridge app.)
5. Select the desired Broadlink device when it comes up, noting that you need to reecord codes to the same Broadlink tha yu will want to send the commands from (for instance if you have them in more than once room).  
6. Enter the device name, with some very specific rules.  For my device handler to work, the device name is not optional as it says here.  This is what I will hopefully be able to skip with a smart app, but for this quick version you still have to learn and specifically name codes for on and off, as follows: Name of device exactly as it will appear in smart things (can include spaces if you want), then a space (important), then either the word "on" or "off" (lower case matters for the words on and off).  Devices are not required to have both on and off commands recorded, but you do have to record separately whichever you want to work, even if both use the same button such as a toggle switch.  See the end of this section for some creative ways to use this feature.
7. Learning the code works like it did in the e-Control app, if you played with that durig setup.  There is a different approach for RF or IR device.  For an IR device bring your remote close to the Broadlink, click "learn code" and then preess the button you want to learn.  The web site will indicate success or not.  For an RF device, bring the remote close the the broadlink, click "frequency scan" and hold down the remote button for several seconds, until the indicator on the top right side stops spinning.  This is not compleltely reliable and may need to be repeated.   After this records, click "learn code" and press the button you want to learn.
8. Repeat steps 6 and 7 for all the devices you want to add.

Here's where some creativity can help, now that you've seen what the steps are.  Even though these are labeled as devices and their on and off switches, they don't need to physically be exactly that.  These can be named as any action you want to put into a smartthings scene or action, or to trigger with the echo by saying "Alexa turn on _____" or "start _____".  It sometimes even responds to "switch to ________" which can be very natural.  For example, you could have something easy like a light switch or outlet controller that does have an on switch and an off switch.  You could also have a TV, where on and off are the same button, but you need to program it in twice, once with the name "on" and once with the name "off" if you want it to respond to both commands.  
You could also get very creative and add any number of things in a way where Alexa can control them.  If you set up a device called ESPN, and its "on button" is programmed to the keystrokes for that channel, your Alexa can respond to "turn on ESPN."  "Turn on the television" for me turns on the TV,  remote HD sender I have and switches the HDMI to the proper input. "Turn to the other input" activates my HDMI switch, or you could program the keystrokes needed on your TV remote.  I programmed in a single fan remote as 3 devices: "low fan," "medium fan" and "high fan."  Each one has its corresponding button set to "on" and the overall remote's "off" switch assigned to all 3.  I also made one just called "fan" and set its off switch as well.  Now I can tell Alexa to turn on the "low fan" or just to turn off the fan.  The possibilities are endless.

## Install this app into SmartThings (finally):
1. Go to Smart Things IDE (https://graph.api.smartthings.com/) and log in. You may need to do this on a computer.  I have difficulty getting it to work right browsing on a phone.
2. Click "my device handlers" and on the page that leads to,  click "create new device handler."
3. Ignore all the default information that comes up, and select the tab that says "from code."
4. Paste in the text from the file in my github called "Broadlink RM Bridge Switch Cloud."
5. On line 48, where it reads uri: "http://xxx.xxx.x.x:xxxx/code/$replaced%20$toggle" you need to manually overwrite the x's with your externaly accessible ip address and port from the RM Bridge app.  This will probably look like yourdomainname.com:7474 or something similar with your specific numbers.  If you entered a password in the RM bridge app, you need to add those to your ip address so it the above would now look like yourusername:yourpassword@yourdomainname.com:7474  where those are your actual user name, password and ip address.  
5. Click the "create" button. 
6. At the top of the code, select "publish" and "for me."
## Add your devices to SmartThings
For each device you want to add, perform the following steps while still in the smartthings IDE (the we site where you added the code):
1. Click "my devices" near the top of the screen.
2. Click "New Device"
3. Give the device the exact same name as you entered in the web site when you were setting up the code learning, but do not follow it with a space or the word "off" or "on" as you did there. (technically you cold naame it something different as the label field is the one the code uses; this will match the name if you leave it blank).
4. Give the device a unique network ID.  It does not matter what this is and you won't need to remember it, but it needs to be present and unique.  I often use some variant of the device name but you can name however works for your network.
5. In the dropdown for device type, select "RM Bridge Switch LAN"
6. Click "create"

Your device should now appear in the SmartThings app and work properly, and you can import it into Alexa for use there.
