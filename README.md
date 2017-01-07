# Control Any Remote Controlled Device via Alexa

## If coming back, please review updated language on choosing dedicated android device (old phone batteries can do bad things!)

## What these apps do:
This set of codes lets you link up many (likely most) of your RF- and IR-controlled devices to smartthings, and in turn to any other services linked to your smartthings account, such as IFTTT or Amazon’s Echo (Alexa).  The total cost of needed items (besides the optional smartthings hub) is around $30-35 (depending on which approach you select) at the time of this writing.  There are three versions of this app, each with separate instructions in additional readme files.  They differ in what additional programs you need and whether you can control via aa SmartThings Hub on your local LAN or via the cloud (potentially less secure and slower but does not require purchasing a SmartThings Hub).  Because of security and the fact that smartthings is hosting the service, I'd recommend the version with the hub, but offer the cloud version to use at your own risk, supposing you know enough about your network's security to decide what to do. 

Because this is focused on Alexa integration, it is limited to switches (on/off only, no dimmers or hi/medium/low, but there are workarounds to control different functions as if they were switches, which I'll describe in each approach's readme). While this will also let you integrate these devices into smartthings scenes and so forth, the individual devices don't look ideal in the smartthings app on their own.  This is because these devices don't report their on/off status and I did not put any effort into trying to mimic that. Someone who wishes to clean that up can certainly fork this code to do so.  If there is interest, I may add other types of devices after this initial code is in use and tested more broadly but probably not until Alexa can handle them.  If I get enough requests for a certain type of device I will give it a try.

## Skill level: 
Intermediate. Need a comfort level with digging through things that appear complicated and troubleshooting possible missteps, if provided enough instructions, which I hope to do here. No programming needed. Must be OK with using a device that comes with a manual in Chinese but is similar to other wifi setup processes.

## What you need for all versions of the code:
1.<a href='http://www.amazon.com/dp/B01A4ZAEN8/ref=pd_lpo_sbs_dp_ss_2?pf_rd_p=1944687722&pf_rd_s=lpo-top-stripe-1&pf_rd_t=201&pf_rd_i=B00PCND59S&pf_rd_m=ATVPDKIKX0DER&pf_rd_r=0DA1Z9FRAG5XQ4ND6HF2'>Broadlink RM</a>.  I purchased and tested this with the RM2+ (pro version) linked here. This should work with other models too, possibly with less functionality in what devices they control, but i don't own one to test.  If anyone gets this working with other models please let me know.

2.	Android device on the same local network as the Broadlink. This could be a dedicated device (I use an old phone) or your phone, but this setup will only work while the Android device is on the same network as the Broadlink and is running the bridge app described under #3 (a battery drainer, so probably want a plugged in Android device). This may also work if the Android is on the local network via vpn, but I have not tested it. You can use this code to operate your devices from outside your network.   It is only the Android "bridge" device that must be on the same network as your Broadlink RM. IMPORTANT UPDATE September 2016: I was using an old Nexus 4 but choose something else.  Please research your device to see how it behaves if left plugged in for long periods.  Likely will work best with an Android TV box, a virtual machine on another computer, or similar setup without potential battery issues.  Search the web for "Nexus 4 battery bulging" to see the very bad phone self-destruction that happened due to leaving it plugged in and running for this app.  Everything else here works fine and any old cheap android box should work if this baattery issue is avoided.

3.	Android app used to “bridge” between the Broadlink and web-based services like smartthings.  This is needed because Broadlink does not publish information that would allow users to directly interface with it.  Other developers have figured out a way around this, so I am not attempting to reinvent it.  One possible app is a free option (called RM Bridge) and the other (RM Tasker) costs just over $5 at the time of this writing but is available for a 7 day free trial.  I had poor results with the security on the RM Tasker app (an Internet pen pal testing this with me was able to access my equipment without my password from outside my network), so I cannot recommend that one unless you control over your LAN with a smartthings hub.  For anyone using either app via the cloud, users are cautioned to test whether the security meets their expectations.  There are also differences in how to set up and use these sets of code, as well as how they integrate multiple Broadlink devices.  Read the separate Readme files for each app to get a feel for which is your best choice.  The main upside to the RM Tasker app is that it integrates with Tasker (an Android app commonly used for automation) if you have interest in also using your Broadlink RM device this way.  This version also works much more simply/reliabl with devices where you want to use multiple remote keys for "on" (for instance to "turn on" a Tv channel by sending several numbers).  I have it working both ways but RM Tasker was made to do it versus me having to create a workaround for RM Bridge.  For that use case I would recommend either RM tasker or using RM Bridge with cloud-based control  Sending multiple LAN commands over a SmarThings Hub is not very reliable.

4.	A free smartthings account.  Get one from the Android app or by going to https://graph.api.smartthings.com/.  You will need to go to this web site anyway, best on a computer, to set up these tools.

5.	A physical remote control for whatever you want to control here.  If you've lost it, you will need to program it into a universal remote.  There is no way to access a list of manufacturer codes with the Broadlink.
	
## Additional things you may need depending on version
1. A SmartThings Hub if you want to control via your LAN.  I have only tried this wiht a V2 hub.  Your hub must support local LAN commands (specifically one called hubaction) for this to work.  
2. An externally accessible IP address and an open port, if you want to control without the hub.

## Options and Files on this site:

The RM Tasker Version with local control was published first, and uses the following files:
- Broadlink LAN SmartApp
- Broadlink Manual device entry
- Broadlinkswitch device handler
- RM Tasker LAN ReadMe

My code for RM Bridge is less developed but works.  Ideally I hope to move much of the device management into a sleek smartapp eventually, but for now am publishing something usable that costs less without the wait.  

The RM Bridge version with local control uses the following files:
- Broadlink RM Bridge Switch LAN
- RM Bridge LAN readme

The version with cloud control uses the following files:
- Broadlink RM Bridge Switch Cloud
- RM Bridge Cloud readme

I also had a functioning version that used RM Tasker via the cloud, but have not recreated and tested it for publication because of the security issues I encountered and the difficulty integrating more than one Broadlink with this app.  If you want this version, pease contact me.
