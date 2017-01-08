# Read the <a href='https://beckyricha.github.io/Broadlink-RM-SmartThings-Alexa/index.html'>main readme</a> for this repository first!
This document contains the setup instructions for the SmartApp version that uses the SmartThings hub for local LAN control and the RM Tasker app as a bridge.

## Set-up your Broadlink RM:
I used the app designed for this device by its manufacturer (e-Control, available in the play store) to set it up and add devices. I also installed it on the same android where the RM tasker is running, as it seemed to most reliably import the codes this way.  I only use this app as a bridge to this setup but it can be installed and run on multiple devices if you also want to control things using the app directly.  It's not bad on its own.  My Broadlink arrived with a manual only in Chinese, but install the e-Control app and follow its instructions to add your broadlink RM device to your wifi network. Don’t worry -the app is in English.  I did not take detailed notes during this section and mine is already set up, but it was like many other apps.

## Add some devices to control to your Broadlink RM:
You might want to read through this whole section before trying one, as both the concept and the steps are important.  To make devices work with this app, you need to set them up in a very specific way.  If you also want to use the broadlink app (which offers many more features) you can set the devices up a second time using their built-in templates for TVs, lights, audio receivers, and so forth.  However, remotes added using these templates will not import correctly into smartthings using this app.  Having them in two places in the Broadlink app does not hurt anything.  

We are going to add devices here and assign them functions that happen when you turn them on and when you turn them off in smartthings. This doesn't need to actually be the power button on your remote.  Let's walk through the steps, and then I will explain some creative ways to use them afterward.  

For each device you want to control:

1. On the main page of the e-control app, click the "+" sign and select "add remote."

2.	A set of templates will be offered.  Select "User-defined."

3.	Select "sort in order."

4.	 A weird bug with this app is your choice is step 3 is now the name of your device.  You'll want to change this by clicking the settings icon in the top right of the screen and selecting "device info."

5.	Change its name and icon as desired and click save.  Note that the name here is whatever function you will want to turn on and off, only one per "remote."  

6.	After saving the name change, you should be back on the main blank page for the device.  Click "+" to add a remote button.

7.	Change the name of the button to either "on" or "off" and press save (not every device will need both but if it's actually a switch to turn on and off then it will)

8.	Get your remote control handy.  Back on the main page, press your new button.  The app will prompt you to enter the code.  Select whether to learn a single remote button or a combo, at your option. 	

9.	If you are using an IR remote, press "learn" and press the remote button as prompted.  If an RF remote, select "sweep frequency" and follow the instructions.

10.	If you are learning a sequence of buttons, each one is the same as step 9.  Press the + sign and follow the instructions for each button.  Note that you can insert timing delays between them, which I found useful for my TV to accept the commands.

11.	Try your new button and make sure it works.

12.	Add another button if desired, remembering that they have to be named "on" or "off" to work with this app.

Here's where some creativity can help, now that you've seen what the steps are.  Even though the broadlink presents this as "remotes" and "keys" they don't need to physically map to that, but can be any action you want to put into a smartthings scene or action, or to trigger with the echo by saying "Alexa turn on _____" or "start _____".  It sometimes even responds to "switch to ________" which can be very natural.  For example, you could have something easy like a light switch or outlet controller that does have an on switch and an off switch.  You could also have a TV, where on and off are the same button, but you need to program it in twice, once with the name "on" and once with the name "off" if you want it to respond to both commands.  

You could also get very creative and add any number of things in a way where Alexa can control them.  If you set up a device called ESPN, and its "on button" is programmed to the keystrokes for that channel, your Alexa can respond to "turn on ESPN."  "Turn on the television" for me turns on the TV,  remote HD sender I have and switches the HDMI to the proper input. "Turn to the other input" activates my HDMI switch, or you could program the keystrokes needed on your TV remote.  I programmed in a single fan remote as 3 devices: "low fan," "medium fan" and "high fan."  Each one has its corresponding button set to "on" and the overall remote's "off" switch assigned to all 3.  I also made one just called "fan" and set its off switch as well.  Now I can tell Alexa to turn on the "low fan" or just to turn off the fan.  The possibilities are endless.

## Set up your Android bridge:
Install the RM tasker app and follow its instructions for importing the codes.  I think you can also set up codes there but I have not tried this.  You could also change the names of some of your codes there (such as if they are not named on and off).  I think this can be done without affecting the Broadlink e-control app, if there are reasons to keep these different, but also have not tested it. Select enable web server.  Leave the web authentication off.  This assumes you are keeping this port closed on your router so you won't need it.  At the bottom of the screen, note the ip address and port where the bridge is operating.  It will be most reliable if you can set your android up with a static ip address, but that is beyond the scope of this tutorial (it can vary for different android devices but is usually accessible under wifi settings by long pressing the name of your wifi network and selecting the advanced options).  

## Install this app into SmartThings (finally):
You need two different bits of code, installed in this order:
1. Go to [Smart Things IDE] (https://graph.api.smartthings.com/) and log in. You may need to do this on a computer.  I have difficulty getting it to work right browsing on a phone.

2. Click "my device handlers" and on the page that leads to,  click "create new device handler."

3. Ignore all the default information that comes up, and select the tab that says "from code."

4. Paste in the text from the file in my github called "Broadlinkswitch device handler."
  a.	Note for advanced users (you know who you are if this applies as it's not most people): If you have set up your own namespace, that needs to be changed manually both in this handler and my smartapp, as it actually gets used in device creation. 

5. Click the "create" button. 

6. At the top of the code, select "publish" and "for me."

7. Select "My SmartApps" and then "New SmartApp."   Similarly to before, click the "from code" tab, paste in the text from my github file called "Broadlink LAN SmartApp" and select "create" but don't need to publish.

8. Select the button above the code that says "app settings" and then a link on the page that comes up called "settings."  There should be two boxes to enter info about your Broadlink device.

9. For "BLURL" enter the ip address and port of your bridge that you wrote down earlier.  It should not include the "http://" so it will probably look something like 192.168.1.xxx:9876 unless you have different network settings or changed the port number.

10. BLMac is the mac address for your Broadlink.  The easiest way to get that, if your RM Bridge app is running, is to go to its web site by entering the same ip address above into a browser.  It has lots of info about your setup.  Copy and paste the mac address version without the colons.

11. Click "update" for these new settings to stick.

12. After the update, click "code" near the top of the window.  

13. To the right or the bottom of the code, depending on your browser, there should be an option where you can select the location.  This must be a location with a hub physically attached to it, on the same local network as your broadlink and bridge, the hub must be turned on and the RM Bridge app must be running. 

14. Select the location, then click "install."  This should create your devices.  

## Troubleshooting:
If anything goes wrong during install or if you add more devices, you can go to this smartapp and run the install again.  This can add new devices and update their codes, but won't automatically update the ip and mac address unless you delete the devices first.  If you uninstall the app, the same way you just installed it, that should remove the devices so you can start fresh so long as all the devices are not attached other things like Alexa, but sometimes does not work.  In the latter case you will need to manually remove devices and install this smartapp again.

In case of further difficulties, I have added another optional smartapp called broadlink manual entry, that lets you edit info for these devices directly.  It can be created as a smartapp by pasting in the code like you did above (it does not need another device handler).  However, this one, unlike the first, works much better on your phone.  (you can do similar things right in the web site if you need to but it is less reliable).  After you paste and save the code, select publish -> for me.  Then in your smartthings app on your phone (described for android, so yours may vary), go to "marketplace" (along the bottom), then the smartapps tab at the top, then scroll to the bottom of that list to "my apps."  "broadlinkmanualentry"  should appear here, so select it. It will prompt you for a device to edit and let you do so.  Click "done" when you are done.  If you needed to add a missing device, you can add it in the IDE (the web site you were using to paste in the codes), but it won't let you enter all the needed codes so you will edit it using this smartapp.

## Using multiple Broadlink RM devices:
If you truly love this but want it to work with more than one Broadlink scattered around multiple parts of the house (they're very cheap) there are ways now to use more than one broadlink, but it will get easier.  Right now the RM Tasker app does not generate codes to say which MAC address each code came from, as it was not really designed for this usage.  That may be in a future update and I can enhance this app then to automate keeping it straight. Meanwhile, I only have one Broadlink so can't test this, but in theory you should be able to add devices as above, except that you need to learn the codes using the Broadlink Device that will be sending them out.  When you import the devices, initially they will all be assigned the mac address you entered into the app settings.  You can use the manual entry code described above to alter the mac address of any devices that should use the other broadlink RM.

## Note for those who want to use pretty device templates in the e-control app

If you want to use the nice device templates in e-control and not make separate on and off buttons, it takes more work but you have two other options. Either way you would need to find the right codes in the RM Tasker app. You can either change the code's name in rm tasker or find the codes you want to link to "on" and "off," and manually enter your device using the manual entry smartapp as described under troubleshooting for missing devices above.

<script src="//z-na.amazon-adsystem.com/widgets/onejs?MarketPlace=US&adInstanceId=316d030e-54f2-4085-bbc4-5ba45c996661&storeId=seniorhacks-20"></script>

<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-89762317-3', 'auto');
  ga('send', 'pageview');

</script>
