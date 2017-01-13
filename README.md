# Control Any Remote Controlled Device via Alexa

## What these apps do:
This set of codes lets you link up many (likely most) of your RF- and IR-controlled devices to smartthings, and in turn to any other services linked to your smartthings account, such as IFTTT or <a href="https://www.amazon.com/gp/product/B01DFKC2SO/ref=as_li_ss_tl?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=merchandised-search-top-2&pf_rd_r=TQYV2353YDED0M7X1P2H&pf_rd_r=TQYV2353YDED0M7X1P2H&pf_rd_t=101&pf_rd_p=19a8c901-9fbf-4092-a3fc-c2acf5c8bb5f&pf_rd_p=19a8c901-9fbf-4092-a3fc-c2acf5c8bb5f&pf_rd_i=9818047011&linkCode=ll1&tag=seniorhacks20-20&linkId=85e32cda5628189143d9475add80ce4a">Amazon’s Echo (Alexa)</a>.  The total cost of needed items (besides the optional <a href="https://www.amazon.com/Samsung-SmartThings-Hub-2nd-Generation/dp/B010NZV0GE/ref=as_li_ss_tl?ie=UTF8&linkCode=ll1&tag=seniorhacks-20&linkId=b46f48982e4f13a2dccf39ba3c3461d1">SmartThings hub</a>) is around $30-35 (depending on which approach you select) at the time of this writing.  There are three versions of this app, each with separate instructions in additional readme files.  They differ in what additional programs you need and whether you can control via a SmartThings Hub on your local LAN or via the cloud (potentially less secure and slower but does not require purchasing a SmartThings Hub).  Because SmartThings is hosting the service, I'd recommend the version with the hub, but also offer the cloud version to use at your own risk, supposing you know enough about your network's security to decide what to do. 

Because this is focused on Alexa integration, it is limited to switches (on/off only, no dimmers or hi/medium/low, but there are workarounds to control different functions as if they were switches, which I'll describe in each approach's readme). While this will also let you integrate these devices into smartthings scenes and so forth, the individual devices don't look ideal in the SmartThings app on their own.  This is because these devices don't report their on/off status and I did not put any effort into trying to mimic that. Someone who wishes to clean that up can certainly fork this code to do so.  If there is interest, I may add other types of devices after this initial code is in use and tested more broadly but probably not until Alexa can handle them.  If I get enough requests for a certain type of device I will give it a try.

## Skill level: 
Intermediate. Need a comfort level with digging through things that appear complicated and troubleshooting possible missteps, if provided enough instructions, which I hope to do here. No programming needed. Must be OK with using a device that comes with a manual in Chinese but is similar to other wifi setup processes.

## What you need for all versions of the code:
1. <a href='https://www.amazon.com/BroadLink-Universal-Remote-Control-RMPRO-US/dp/B01FJMBM8M/ref=as_li_ss_tl?_encoding=UTF8&psc=1&refRID=EWXC2F49XBNYPNKZ6X0C&linkCode=ll1&tag=seniorhacks20-20&linkId=c97026595ab5c4e4f0ec4c2a0d545b4e'>Broadlink RM</a>.  I purchased and tested this with the RM2 pro version linked here. This should work with other models too, possibly with less functionality in what devices they control, but I don't own one to test.  If anyone gets this working with other models please let me know.

2.	Android device on the same local network as the Broadlink. This could be a dedicated device (I use a <a href='https://www.amazon.com/gp/product/B01LCQNWNM/ref=as_li_ss_tl?ie=UTF8&psc=1&linkCode=ll1&tag=seniorhacks20-20&linkId=1eaf649f894967fe6755217e0d41e9bd'>cheap android box</a>) or your phone, but this setup will only work while the Android device is on the same network as the Broadlink and is running the bridge app described under #3 (a battery drainer, so probably want a plugged in Android device). This may also work if the Android is on the local network via vpn, but I have not tested it. You can use this code to operate your devices from outside your network.   It is only the Android "bridge" device that must be on the same network as your Broadlink RM. IMPORTANT UPDATE September 2016: I was using an old Nexus 4 but choose something else.  Please research your device to see how it behaves if left plugged in for long periods.  Likely will work best with an Android TV box, a virtual machine on another computer, or similar setup without potential battery issues.  Search the web for "Nexus 4 battery bulging" to see the very bad phone self-destruction that happened due to leaving it plugged in and running for this app.  Everything else here works fine and any old cheap android box should work if this baattery issue is avoided.

3.	Android app used to “bridge” between the Broadlink and web-based services like smartthings.  This is needed because Broadlink does not publish information that would allow users to directly interface with it.  Other developers have figured out a way around this, so I am not attempting to reinvent it.  One possible app is a free option (called <a href='https://play.google.com/store/apps/details?id=de.fun2code.android.rmbridge&hl=en'>RM Bridge</a>) and the other (<a href='https://play.google.com/store/apps/details?id=us.originally.tasker&hl=en'>RM Tasker</a>) costs just over $5 at the time of this writing but is available for a 7 day free trial.  I had poor results with the security on the RM Tasker app (a friend testing this with me was able to view the MAC of my Broadlink without my password from outside my network), so I cannot recommend that one unless you control over your LAN with a smartthings hub.  For anyone using either app via the cloud, users are cautioned to test whether the security meets their expectations.  There are also differences in how to set up and use these sets of code, as well as how they integrate multiple Broadlink devices.  Read the separate Readme files for each app to get a feel for which is your best choice.  The main upside to the RM Tasker app is that it integrates with Tasker (an Android app commonly used for automation) if you have interest in also using your Broadlink RM device this way.  This version also works much more simply/reliably with devices where you want to use multiple remote keys for "on" (for instance to "turn on" a Tv channel by sending several numbers).  I have it working both ways but RM Tasker was made to do it versus me having to create a workaround for RM Bridge.

4.	A free smartthings account.  Get one from the Android app or by going to <a href='https://graph.api.smartthings.com/'>the SmartThings developer site</a>.  You will need to go to this web site anyway, best on a computer, to set up these tools.

5.	A physical remote control for whatever you want to control here.  If you've lost it, you will need to program it into a universal remote.  There is no way to access a list of manufacturer codes with the Broadlink.
	
## Additional things you may need depending on version
1. A <a href='https://www.amazon.com/Samsung-SmartThings-Hub-2nd-Generation/dp/B010NZV0GE/ref=as_li_ss_tl?ie=UTF8&linkCode=ll1&tag=seniorhacks-20&linkId=b46f48982e4f13a2dccf39ba3c3461d1'>SmartThings Hub</a> if you want to control via your LAN.  I have only tried this with a V2 hub.  Your hub must support local LAN commands (specifically one called hubaction) for this to work.  
2. An externally accessible IP address and an open port, if you want to control without the hub.

## Options and Files on this site:

The <a href='https://beckyricha.github.io/Broadlink-RM-SmartThings-Alexa/RM%20Tasker%20LAN%20ReadMe.html'>RM Tasker Version with local control</a> was published first, and uses the following files:
<ul>
<li><a href='https://github.com/beckyricha/Broadlink-RM-SmartThings-Alexa/blob/master/Broadlink%20LAN%20SmartApp'>Broadlink LAN SmartApp</a></li>
<li><a href='https://github.com/beckyricha/Broadlink-RM-SmartThings-Alexa/blob/master/Broadlink%20Manual%20device%20entry'>Broadlink Manual device entry</a></li>
<li><a href='https://github.com/beckyricha/Broadlink-RM-SmartThings-Alexa/blob/master/Broadlinkswitch%20device%20handler'>Broadlinkswitch device handler</a></li>
<li><a href='https://beckyricha.github.io/Broadlink-RM-SmartThings-Alexa/RM%20Tasker%20LAN%20ReadMe.html'> RM Tasker LAN ReadMe </a></li>
</ul>
The <a href='https://beckyricha.github.io/Broadlink-RM-SmartThings-Alexa/RM%20Bridge%20LAN%20Readme.html'>RM Bridge version with local control</a> uses the following files:
<ul>
<li><a href='https://github.com/beckyricha/Broadlink-RM-SmartThings-Alexa/blob/master/Broadlink%20RM%20Bridge%20Switch%20LAN'>Broadlink RM Bridge Switch LAN</a></li>
<li><a href='https://beckyricha.github.io/Broadlink-RM-SmartThings-Alexa/RM%20Bridge%20LAN%20Readme.html'>RM Bridge LAN readme</a></li>
</ul>
The <a href='https://beckyricha.github.io/Broadlink-RM-SmartThings-Alexa/RM%20Bridge%20Cloud%20Readme.html'>version with cloud control</a> uses the following files:
<ul>
<li><a href='https://github.com/beckyricha/Broadlink-RM-SmartThings-Alexa/blob/master/RM%20Bridge%20Switch%20Cloud'>Broadlink RM Bridge Switch Cloud</a></li>
<li><a href='https://beckyricha.github.io/Broadlink-RM-SmartThings-Alexa/RM%20Bridge%20Cloud%20Readme.html'>RM Bridge Cloud readme</a></li>
</ul>
I also had a functioning version that used RM Tasker via the cloud, but have not recreated and tested it for publication because of the security issues I encountered and the difficulty integrating more than one Broadlink with this app.  If you want this version to play with, it's on the repo but not supported.  Find it <a href='https://github.com/beckyricha/Broadlink-RM-SmartThings-Alexa/blob/master/tasker_cloud_version'>here</a>.


<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-89762317-3', 'auto');
  ga('send', 'pageview');

</script>
