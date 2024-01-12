# How to build a C-Band ground station.   
   
Navigation: [home](README.md)  

C-Band is the most difficult aspect of setting up and running a full satcom ground station, but because of this and the rich data it can provide, if you have the space, time and patience its probably the most rewarding of all the AERO frequencies that are in use.   
I have seen many examples where having both C and L band data from the same Inmarsat has proven very effective, to the point of exciting, to see both sides of the avionics or aircrew / dispatch is just thrilling when it all comes together and works seamlessly.   

Here is a random screen shot of the aircraft that my dish can pick up over the course of a day - you get an ebb and flow in the traffic you will see depending on the time of day and year. The mix of military vs civil will also change just like it does with ADSB.   

   <img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/72hourscband98w.png" height="400">     

To see what Inmarsat satellite(s) are over your location, review the [Inmarsat](Inmarsat.md) page. This step is critical and not optional for a C-Band setup. You will need a very clear view of the satellite over its entire orbit. It will need to be well above the horizon at all times and it will need to be clear of all terrestrial obstructions at all times.   

## Start slowly.   
It can be overwhelming and seem impossible to build a high performance C-Band ground station, but the truth is, you can start simple and just solve each issue as you feel the need. You don't have to do everything outlined on this page in a week. The other nice thing about this page is that you don't have to re-invent the wheel. You can just check things off the list as you go.   
Lets break it down....    
1. Find your satellite and make sure you have a good spot on your property to place the dish.
2. Get some basic (Node-RED) graphing of the satellite orbit running.
3. Buy a dish.
4. Buy a feed (LNB), LNB power supply, some TV grade coax cable, SDR, computer.
5. Get planes on a map.
6. Get aircraft ACARS messages.
7. Move the dish twice a day (for example, once before work, once after work). Get a feel for where you need to point the dish for each part of the satellite orbit, ie, top and bottom.    
8. When you are sick of retuning your SDR frequencies for hot/cold (ie, day/night) cycles, buy a GPSDO and modify the LNB so you no longer have re-tune the SDR frequencies. Or ensure you buy an external LO LNB from the start and never have this issue.
9. When you are sick of manually moving the dish, put a linear motor on it to track the satellite automatically.   
10. Done. Sit back and enjoy the data. (Be aware, this last step could take a few years to get to - no, not kidding).

## Dish size matters.
You will need the space for a minimum of a 6ish foot (2.4 meter) dish. Some people will tell you that you can get away with a smaller dish, but the signal is going be so marginal that its hard to justify the time and money to setup something might only just work or will be frustrating to use. You may even end up either giving up, or buying a bigger dish, ie spending needless money on the smaller dish.      
I also feel that most people will want a large enough dish that _all_ signals from the satellite can be recovered around the clock. If you are close to the equator (ie, under the satellite) then yes, perhaps something smaller might work.  
Do your research, ask lots of questions from those that insist a smaller dish will 'work just fine', qualify their data quality.    
Be sure and read this entire page before making the final decision of the final dish size, there are _three_ types of AERO Data from C-Band (10500, 1200 and 8400) and most people with smaller dishes only can pick up one (10500), they dismiss the other two with a wave of the hand 'There is nothing interesting using those weaker signals' ... You need to make that decision, not them ....   

Having free and easy physical access to the dish is also important, you will be spending a lot of time working on it and adjusting it for the setup / commissioning period at all hours of the day and night. If it is on a roof where access is uncomfortable or dangerous in the dark, that is a no-go in my mind. You will need also run a coax and a few command and control cables to the dish and lastly some sort of power outlet or stable low voltage outlet will be required somewhat close to the dish.   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/benadjustingdish.jpg" height="580">  
   
### Dish computer
You will also need a fairly powerful Windows PC or Linux computer to run Node-RED, the SDR software and Jaero on. This does not need to be next to the dish, but you will need to run the coax and perhaps other cables from the general area of the computer location to the dish. Something around i5 to i7 with 8-16 gig of RAM and an SSD - so anything from the past few years should be fine.  
   
## Graph / Plot the Satellite Orbit
You can actually start with the software aspect before you buy any hardware.   
A critical aspect of setting up and tuning the dish is to be able to visually see the satellite orbit on a graph so that when you power up the dish tracking, you already know the different parts of the satellite orbit and this will speed up your alignment process.   
Recall from the [Inmarsat](Inmarsat.md) page that the orbit moves in a figure 8 pattern in the sky. Both of these movements (elevation at the very least) will need to be tracked over the 23 hour 54 minute orbit period of the satellite in order to keep the aircraft data flowing around the clock.  
Here is this orbit in the sky as a reminder:  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/98Wsatorbit.PNG" height="250"> 
    
This can be hard to visualize and keep track of, so a more conventional graph is critical (and in my experience not optional):  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/98worbitgraph.png" height="200"> 
   
This is the graph that you will be spending a lot of time looking at.   
The period of the graph at first should be pretty corse, at least 1 day, 2 at the most. If you want to track long term (monthly or longer) or short term (say a few minutes) you can, but be sure and have two versions of this graph, short and long period. I would not go less than a day since that is the orbit period and you will need some reference of time around that window.  
In this image, the red plot is the elevation and the green is azimuth. Note the double dip in the azimuth. We will come back to this shortly.   
 My hope is that seeing the '8' graph and this graph next to each other will help you visualize the pattern your dish needs to track over the course of each daily cycle.  
 This graph will also help you understand that if the top of the orbit is around 11am, then it will be at the bottom of its orbit around 11pm, but only for a few weeks at at time, because its over a 23 hour 54 minute orbit, it will slowly drift, and so in a few months you will see the top/bottom time of the orbit move an hour or so.   

I highly recommend you spend some time setting up this graph in either Node-RED or some other stable graphing software. You will need it running around the clock.
This graph is critical to the ADSC ground station operator as it will show when the satellite is at the top of its orbit and at the bottom of its orbit and when the satellite is at the most left part and right part of its orbit. These are two very critical points of the orbit and you will be adjusting the dish at these points, so knowing ahead of time that you will need to setting an alarm for something like 3am and 3pm is very important.   
Optional, but to give you an idea of how important this whole orbit data is, here is a snip from the webpage status I have built to keep tabs on the dish and orbit data. You don't have to go this hard-core, but I find it very important to know and see this data:    

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/98wdishstatus.png" height="380">   

## Auto update TLE
Before we leave the graph / where is the satellite topic, its also critical that you are working with fresh TLE (Two Line Element) data for your satellite. By fresh, I have found that updating them every 24 hours is about right. I was doing it monthly for a while, but feel I have better 'lock' on the sat with 24 hour TLE. I have an example flow to get you started on this auto-update via Node-RED on the [autoTLE](autoTLE.md) page.   
    
## Hardware BOM (Bill of materials)  
1 x 2 meter (6 foot) C-Band satellite dish (Can be larger, but not smaller) Try and find a used C-Band TV dish. They can be found 2nd hand cheap from places like Facebook Marketplace and Craigslist in USA and places like that in other countries. [eBay](https://www.ebay.com/b/c-band-dish/bn_7024908961) I'd love an 8 foot if I was going to do it again and if I had the space, 10 to 12 foot. More than that would be beyond the point of diminishing returns.   
1 x 75 ohm TV coax cable. Triple or quad shield, length for your installation. [Amazon](https://www.amazon.com/s?k=75+ohm+outdoor+coax+cable&ref=nb_sb_noss)   
1 x Low Noise Block (LNB). Note, in the past we used Titanium LNBs, the original model is no longer sold and the new (2023+) model is not able to receive ADSC signals.   
norsat 3.4Ghz to 4.2Ghz with external 10Mhz LO. There are different models (N type and F type connectors). Get used, new is too expensive.   
1 x Bias Tee diplexer. The norsats require ~20v DC and 10Mhz mixed and fed down the coax and the signal RF only to be split out for the SDR. Example: Mini-Circuits ZABT-2R12G+ (950Mhz to 2150Mhz).  
1 x dielectric. Small bit of blank (no copper on either side) circuit board or teflon. About the size of a matchbox but thinner. Needs to pressure fit in the throat of your waveguide to convert the mono LNB feed to circular (not optional - critical!!!).    
1 x Scalar ring / choke. The norsat LNBs do not include a wave guide. Get one to match your dish F/D ratio.    
1 x power injector. 18 to 21 volt. High quality. Must have very low switching noise if switch mode.   
1 x RTLSDR v3 dongle. (Silver or black flat rectangle shape one). Get the real thing from [RTL-SDR](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/). V4 is snake oil. Do not buy.  
1 x Computer (Junk store - aka your garage)  
1 x GPSDO module [Leo Bodnar](http://www.leobodnar.com/shop/index.php?main_page=product_info&cPath=107&products_id=301&zenid=7527c5a77e36a6c7028130804877017c)   
1 x power cable for motors and 5v DC supply for GPSDO - length for install [something like this](https://www.amazon.com/Multi-Core-Shielded-Anti-Interference-Control-Signal/dp/B09639HGN9)   
1 x Linear motor with resistance position feedback. Stroke length as per instructions [4'' example from Amazon](https://www.amazon.com/gp/product/B00NVI5RII/).  
1 x Microcontroller with 5 amp H-Bridge relays [Example from Amazon](https://www.amazon.com/s?k=h-bridge&ref=nb_sb_noss_1).   

## Physical setup   
Now that we accurately know where the satellite is and what time it is, we can start to set up the dish feed horn and pick up the 10500 signal.
Once you have the LNB mounted on the scalar ring and the ring mounted to the three arms on the dish, run the coax cable back to the power supply and diplexer.
The LNB needs around 18v to 21v DC to operate, this voltage will blow up your SDR dongle if you apply that voltage to it, so you need the diplexer to mix the 10Mhz GPSDO LO (Local Oscillator) and DC and send that to the LNB, but then to pass the just RF signal and block the voltage to the SDR.   
Here is a condensed example of how the norsat is setup with the diplexer. There is no power supply here or SDR, but it should give you an idea of how the LNB and diplexer work together.   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/exampenorsatconfig.png" height="480">   

   
Ok, so the LNB is powered up so now bolt the waveguide to the LNB and attach the scalar ring to the dish.    
Here is an example.     
   
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/norsatondish.png" height="320"> 

 
If not already, place the dish pretty much in its final resting place. It should be level at the base in both axis. This is important because as you track in elevation, you don't an an azimuth component creeping in as it will move you off signal.    

Don't secure the dish to the ground yet, you will need to pivot it to find the middle of the orbit. Look at the graph and see where the satellite is in its orbit and move the dish left and right while looking at the waterfall to find the edges of the signal.   
     
It should go without saying, but clearly don't do this initial setup on a windy day and be sure to have a plan to mount the dish to the motor and mounted with enough cement to survive your once every 100 year wind storm.

I put a tent peg in the ground and used a marker to show the edges of the orbit. Just use any method that works for you setup. You just want to be able to have top bottom left right marks for each of the 4 parts of the satellite orbit clearly defined so any mechanical limits / hard stops can be avoided.... This is more important than it first seems. The satellites do have a very long period drift. It takes a lot of fuel to keep them on station, so they ballance the life the satellite fuel with performance. That means how you set up the dish this week might be different in a month, in 6 months, in a year. You want to ensure you have plenty of free movement beyond just where the satellite is located right now.  

### SDR software.   

This is a bit of a thorn in our side at the moment. In time we will move to [SDRReceiver](SDRReciver.md) but for now the quickest way to get going is to use SDR# or SDR-Console.  
Download it, unzip it and run the bat file to set up the SDR.  
Then run zadig as admin and install the driver for the SDR.  
Now run the SDR software.  
Next, finding the right frequency. This has been pretty hard in the past since its hard to find an image of what you are looking for on the web. I am trying to get screen shots of all the Inmarsats so people know where to look and what they are looking for.
Here is 98W 10500 burst waterfall.  All the Inmarsats ADSC look just like this. Just the frequency changes by a little. You should be able to see a pattern like this on every sat pretty close to this downconverted frequency. Note the small chirpy R and T channels on the left, they are of some value, but the bulk of the interesting data is in those big fat 10500 bursts, so focus on finding them for now.   
  
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/10500clean.gif" height="350">  
      
From this waterfall we are not going to try and decode aircraft just yet (I know, your excited and want to see aircraft on a map, but that will come).  
Try moving the horn in and out of the dish and moving the LNB dielectric around in the feed and seeing if you can get a better signal strength. the dielectric should be as far forward in the choke as you can and generally is perpendicular to the LNB feed.   
Even if the dish is not perfect on sat, you can still try and peak the LNB, then peak the dish, then peak the LNB and just iterate a few times to get a good clean signal.   

## Azimuth Alignment
Now is when the graph starts to come into play. We are first going to look at the graph and find the time when the azimuth is at its peak. We will then go outside with a laptop or computer that can view the waterfall and move the dish side to side and ensure the signal is peaked up left to right.   
Tip, move the dish right till you just lose the signal, mark it, move it to the left, mark it. Now you know where the azimuth is located for the left (or right) for that part of the orbit. Now wait 12 hours when the satellite is at its right (or left) most and do the same again, move till loss of signal, mark, move the other way till loss, mark and find the middle.   
Now move the dish to the middle of those two master marks.   
Congratulations your dish is now azimuth aligned. Don't lock it down too firm, but well note and roughly fix the dish to the ground at that position.   

## Elevation Alignment
This is the critical one.   
With the dish roughly on signal you need to find a yardstick or stable measurement ruler than can remain in place for a few weeks. It should be a solid datum point that you can measure the tilt of the dish against. It should not interfere with the movement of the dish at all and should not be in the way of the linear motor that you will be mounting. You should be able to draw on it and thus mark the top and bottom of the orbit in elevation. It can be behind the dish or in front, perhaps at the front rim/lip.   
You will need to be as accurate as possible here. Depending on your look angle to the satellite will determine how much your dish will need to pivot up and down to track the sat.  
It could be as small as an inch (25mm) or up to 3-4 inches (75+mm). Thus you need to be as accurate as possible in your marks. (The angle and movement are based on your location in relation to the satellite - for example, the closer to the equator you are, the more your dish will be looking up - if you live closer to the poles, your dish will be looking more at the horizon.)   
## Find top and bottom of the orbit on the dish   
Over 48 or more hours, look at the graph and pick times when the satellite is at the top and bottom of the orbit.  

This is critical and not optional. Mark the dish position with a marker on your yardstick, note the top of the orbit position and 12ish hours latter, the bottom of the orbit position. Yes, this means you will be going outside in the dark more than a few times. Hence my comment about having free easy access to the dish.    

Once you have these two points clearly and repeatable defined, measure the distance between them.  
Generally it will be around 2 inches (50mm) it can be more, it can be less, but that is roughly the sort of movement we are finding is necessary.   
Now purchase a linear actuator that will cover at least the distance you measured. You can go a little longer, but not much, you don't want to lose resolution.  
Next purchase a 6v DC power supply. The arms are all generally 12v (Some are 24v DC, so be sure and check). At 12v the arm moves WAY too fast, at 5v the motor does not have enough power to move the dish. Note, its 5v for a 6 foot dish, if you have a bigger or smaller dish you will need to experiment. If you have a different motor, you will need to experiment. The key is that it has enough power, but is slow enough to be controlled.  
It is CRITICAL that the actuator is the type that has a position feedback resistor. NOT just end stops and not just 'Im turning pulses', but gives a resistance feedback based on the current position.  
Some linear motors only give a pulse output as the motor spins, you *do not* want this type of actuator. ONLY buy the type of motor/arm that has a resistor position indicator. Using this type will show you the position of the arm and thus dish at all times. You will not need to drive the dish 'home' to re-calibrate it, you will always know the exact position of the arm by the resistor value you measure.   
The resistance feedback linear motors are around the exact price as the others, so don't skimp a few dollars.

Node-RED is outputting the elevation position, we need to remap that to match the position required by the dish.   
The satellite, we know from the graph, moves +-3.2 deg, but what does that translate to on the back of the dish and what does it map to in ohm from the linear motor?   
Node-RED has a 'rescale' node, you send it the +-3.2 deg and it rescales it to the resistance of the linear actuator position (say from 2k Ohm to 5k Ohm).
Now you need to link Node-RED to the actuator.   

## Tracking motor  
Here I used an industrial microcontroller, but you could use an Arduino that has a Cat 5 network port.   
Write some code that takes the Node-RED position (Sent every 15 minutes) and compares it with the current resistance value.  
Move the dish via relays in a H-Bridge in the correct direction with a small dead-band so that the arm does not hunt continuously around the required set point.
Thus every 15 minutes the dish motor will receive a new position from Node-RED NORAD TLE and will move the arm to the new location.   
Now, to sync all this up, put the arm on your desk on some paper marked with the length you measured off the yardstick on the dish.  
You now have a mark for the top of the orbit and bottom of the orbit.  
You can simply wait ~12-24 hours watching the actuator on the desk and your graph and make slight adjustments to your microcontroller code and the Node-RED rescale node to ensure the graph to actuator arm match.


Now when it comes time to mount the arm, it's critical that things match up once again.
Pick a time when the sat is at the top or bottom of the orbit.   
Make sure the actuator is at the top or bottom of its stroke.   
Measure the position of the dish independent of the adjustable arm.   
Now mount the motor arm to the dish in that position. Make sure the arm is very securely mounted to the dish, but can still pivot as the dish moves up and down. Grabbing the top of the dish and moving it up and down should have very little slop.   
In 15 minutes time, your dish will be tracking the satellite very accurately.
   
__tl:dr__ From the graph find the times of the left and right position of the satellite orbit and match it using the SDR waterfall by twisting the dish left right.   
From the graph find the times of the top and bottom of the satellite orbit and match it with the dish using the SDR waterfall by moving the dish up and down (tilt).    
Program the motor to move up and down the exact same range. Bolt it to the dish.   
    
 # Software   
SDRReceiver is hard to setup on C-Band as most people like to see the waterfall as they setup each of the VFOs.
Buy a copy of VAC so you can remove the audio watermark and have more than 3 virtual audio cables.   
Use sdr-console. Put a VFO over each data channel. Assign a different VAC Line number to each VFO. Map/link that audio line number to each Jaero.   
Configure Jaero for zero logging and uncheck local audio decoding. (Uses way less CPU).    
Configure each jaero basestation output for a different port number in either VRS or readsb.   
Configure all the Jaeros to use the same ACARS feed IP and port (say into Node-RED) for the ACARS. Please consider adding a second feed (type 'dumpJSON') to airframes.io.      
    
The 1200 burst data has a lot of small bizjet and military aircraft on it. Its a very tricky collection of channels to pickup since there are a lot of them and some are not carrying ADSC/ACARS data.   
Here is an example screenshot.
    <img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/1200example.png" height="350">   
   
Once again each VFO here has a matching VAC and matching Jaero. This is in addition to the 10500 VFO/VAC/Jaeros you will be running. (Now you can better see why a fairly powerful computer is required for C-Band).   
    
# Jan 2024 LNB update   
The Titanium LNB we were using for many years are no longer built.   
Its important to note that both Titanium and norsat LNBs are not, were not, made _for_ ADSC work. It was just nice that we could (abuse) their primary TV use for ADSC reception.    
Part of the reason that model is no longer made or sold is that 5G cell phones are very close to the 3.4Ghz ADSC frequencies and there is a strong chance of getting 5G interference. The new model Titanium LNB has a 5G filter that very aggressively filters out the weak ADSC signal. Also the new version LNB can not be modified for the GPSDO clock.   
norsat also offer a 5G blocking LNB, I have not tested those and don't plan to at this stage (its very expensive to just buy these LNB for quick pass/fail tests). The non 5G filtered ones are working Ok. I have heard of some ADSC installations have so much 5G interference that they have had to shut down.   
    
All that said, I am going to leave these old photos and details about replacing the crystal with the external 10Mhz GPSDO signal as it served us well for many years and could be of use for other applications.   

# GPSDO (GPS Disciplined Oscillator) Modified LNB    
The LNB works great for big fat wide TV signals, but for the narrow ADSC signals the thermal drift in the 25 Mhz crystal clock is too much and the downlink data will drift outside of the SDR software VFO. (And its critical (as in not optional) for the very narrow 1200 burst data).   
The way to fix this is to replace the crystal with a GPS clock signal that is rock solid no matter what the temperature.   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/titaniumlite.jpg" height="350">   
   
   The Titanium Lite LNB is pretty sweet as it does not have any filtering and will go down to the required 3.4Ghz easily. Its also very simple to open up and modify.   

This is not the exact chip used, but its the closest block diagram I could find, it gives you the idea of what we need to do. Remove the chip and inject a clock signal at the same frequency.   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/lnbblockdiagram.png" height="250">   
     
   Here is the kit you will get from Leo.    

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/gpsdokit.jpg" height="250">   

You will also need to download and run Leo's USB tool kit to adjust the clock to 25 Mhz. Here is a screen shot of the settings I am using.    

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/gpsdousbsettings.jpg" height="650">   

The GPS antenna just needs a clear shot of the sky and it does not need to be close to the dish as its not about position, but clock (the very accurate one pulse per second that the GPS send down).    
Ok, so with the GPSDO setup and the LNB in hand, remove the top cover and lets take a look at the crystal we need to remove.    

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/crystalbeforeremoval.jpg" height="450">   

Heat each end up and pry the cyrstal off the PCB. Be careful not to use too much heat and lift the tracks, just ease the crystal off by heating each end back and forth quickly.    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/crystalafterremovalwithspares.jpg" height="550">   

Here is the crystal removed and added to the pile of others that I have done for other people and for testing different LNB's on my dish.    

Next up, drill a hole in the LNB for the clock coax.    
I used to drill it in the top next to the existing one, but now drill the hole in the bottom and it works much much better. There is less to waterproof and the coax does not have as much strain on it.   
Here is the old top method.    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/bothcoaxfrombehind.png" height="250">    
One thing to be very careful about!!!! When you drill from either side, be super slow and careful. Here is a photo from a guy that did the mod on his LNB and totally (well, pretty much) destroyed it.    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/carefuldrillingcoaxhole.png" height="350">    
Ok, so with the hole drilled up from the bottom, thread the coax into the LNB.    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/coaxready.jpg" height="250">    
Strip and tin a short bit of both shield and center and then scratch a little of the ground coating off the PCB for the shield to solder to. Solder the shield to the board and the center of the coax to either of the crystal pads. Note, it does not seem to matter which of the crystal pads you put the center to, I have tried both and it works the same no matter. Here are some example shots of how it will end up looking, top or bottom coax method also does not matter, but top will require good waterproofing and some cable management so it does not bend too sharp.    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/coaxandcenter.png " height="350"> <img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/coaxconnection.jpg" height="350"> <img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/fatcoax.png" height="350">   
Ok, so that should give you the idea of whats needed. Lastly, while you are in the LNB, just take a close look at the main coax connector. I have found 3-5 LNBs with either open circuit or poor dry joints on this connector and its more than worth your time to inspect this joint and touch it up if needed.    
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/commonproblem.png" height="250"> <img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/dryjointonconector.png" height="250">   
Ok, so now very very carefully screw the lid back on cCarefully because the aluminum is super soft and its easy to strip the bolts) and enjoy that sweet sweet drift free signal.


<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>