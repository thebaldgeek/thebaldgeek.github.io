# How to build a C-Band ground station.   
   
Navigation: [home](README.md)  

C-Band is the most difficult aspect of a satcom ground station, but because of this and the rich data it can provide, if you have the space, time and patience its probably the most rewarding of all the AERO frequencies that are in use.   
Here is a random screen shot of the aircraft that my dish can pick up at a pretty average time - you get an ebb and flow in the traffic you will see depending on the time of day and year.   

   <img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/98wonly.png" height="420">     

To see what Inmarsat satellite(s) are over your location, review the [Inmarsat](Inmarsat.md) page. This step is critical and not optional for a C-Band setup. You will need a very clear view of the satellite over its entire orbit. It will need to be well above the horizon at all times and it will need to be clear of all terrestrial obstructions at all times.   
You will need the space for a minimum of a 6 foot (2 meter) dish. Some people will tell you that you can get away with a smaller dish, but the signal is going be so marginal that its hard to justify the time and money to setup something might only just work. I also feel that most people will want a large enough dish that all signals from the satellite can be recovered around the clock. If you are close to the equator (ie, under the satellite) then yes, perhaps something smaller might work. Do your research, ask lots of questions from those that insist a smaller dish will 'work just fine', qualify their data quality. Be sure and read this entire page before making the final decision of the final dish size, there are three types of AERO Data from C-Band and most people with smaller dishes only can pick up one, they dismiss the other two with a wave of the hand 'There is nothing interesting using those' ... Moving on....   
 Having free and easy physical access to the dish is also important, you will be spending a lot of time working on it and adjusting it for the setup / commissioning period. If it is on a roof where access is uncomfortable or dangerous, that is a no-go in my mind. You will need also run a coax and a few command and control cables to the dish and lastly some sort of power outlet or stable low voltage outlet will be required somewhat close to the dish.   

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/benadjustingdish.jpg" height="580">  
   
You will also need a fairly powerful PC or Linux computer to run the SDR software and Jaero on. This does not need to be next to the dish, but you will need to run the coax and perhaps other cables from the general area of the computer location to the dish. Something around i5 to i7 with 16 gig of RAM and an SSD - so anything from the past few years should be fine.  
## Graph / Plot the Satellite Orbit
You can actually start with the software aspect before you buy any hardware.   
A critical aspect of setting up and tuning the dish is to be able to visually see the satellite orbit on a graph so that when you power up the dish tracking, you already know the different parts of the satellite orbit and this will speed up your alignment process.   
Recall from the [Inmarsat](Inmarsat.md) page that the orbit moves in a figure 8 pattern in the sky. Both of these movements (elevation at the very least) will need to be tracked over the 23 hour 54 minute orbit period of the satellite in order to keep the aircraft data flowing around the clock.  
Here is this orbit in the sky as a reminder:  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/98Wsatorbit.PNG" height="250"> 
    
This can be hard to visualize and keep track of, so a more conventional graph is critical (and in my experience not optional):  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/98worbitgraph.png" height="250"> 
   
This is the graph that you will be spending a lot of time looking at.   
The period of the graph at first should be pretty course, 1 or 2 days at most. If you want to track long term (monthly or longer) you can, but be sure and have two versions of this graph, short and long period. I would not go less than a day since that is the orbit period and you will need some reference of time around that window.  
Just to keep you on your toes, the titles of this graph are wrong red line is the latitude (elevation) and the green line is the longitude (azimuth). My hope is that seeing the '8' graph and this graph next to each other will help you visualize the pattern your dish needs to track over the course of each daily cycle.  

I highly recommend you spend some time setting up this graph in either Node-RED or some other stable graphing software. You will need it running around the clock.
This graph is critical to the ADSC ground station operator as it will show when the satellite is at the top of its orbit and at the bottom of its orbit and when the satellite is at the most left part and right part of its orbit. These are two very critical points of the orbit and you will be adjusting the dish at these points, so knowing ahead of time that you will need to setting an alarm for 3am and 3pm is very important. 
## Auto update TLE
Before we leave the graph / where is the satellite topic, its also critical that you are working with fresh TLE (Two Line Elements) for your satellite. By fresh, I have found that updating them every 24 hours is about right. I was doing it monthly for a while, but feel I have better 'lock' on the sat with 24 hour TLE. I have an example flow to get you started on this auto-update via Node-RED on the [autoTLE](autoTLE.md) page.

Now that we accurately know where the satellite is and when, we can start to set up the dish feed horn and pick up the 10500 signal.
The feedhorn we use is the Titanium Satellite C1-PLL Lite. It is important to use this exact feed horn for two reasons.
1. It will down convert the C-Band signal. This is important. Most LNBs are built for TV C-Band, the ADSC signal is at the bottom of the band, so most LNBs will not pick up the C-Band signal this low in frequency.
2. It can be easily modified for the GPSDO. (Global Positioning System Disciplined Oscillator). More on this in a moment.

Once you have the LNB mounted, run the coax cable back to the SWM power supply.
The LNB needs around 18v to 21v DC to operate, this voltage will blow up your SDR dongle if you apply that voltage to it, so you need the SWM power supply to pass the RF signal and block the voltage.  

<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/swmandsdr.png" height="250">   

   
Ok, so the LNB is powered up and the system is ready to go.   
If not already, place the dish pretty much in its final resting place. It should be level at the base in both axis. This is important because as you track in elevation, you don't an an azimuth component creeping in as it will move you off signal.  

Don't secure the dish to the ground yet, you will need to pivot it to find the middle of the orbit. Look at the graph and see where the satellite is in its orbit and move the dish left and right while looking at the waterfall to find the edges of the signal.  

I put a tent peg in the ground and used a marker to show the edges of the orbit.  

### SDR software.   

This is a thorn in our side at the moment. 
The quickest way to get going is to use SDR#.  
Download it, unzip it and run the bat file to set up the SDR.  
Then run zadig as admin and install the driver for the SDR.  
Now run SDR#.  
Next, finding the right frequency. This has been pretty hard in the past. I am trying to get screen shots of all the Inmarsats so people know where to look and what they are looking for.
Here is 98W. 10500 burst frequency and signal.
  
<img src="https://raw.githubusercontent.com/thebaldgeek/thebaldgeek.github.io/main/img/cband/adscFirstLight.png" height="250">  
    
This is a screenshot of my very first ADSC signal, its super weak and scratchy, but I include it to show where you might also start out.  
From this waterfall we are not going to try and decode aircraft just yet (I know, your excited and want to see aircraft on a map, but that will come).  
Try moving the horn in and out of the dish and flipping the LNB dielectric between the two slots in the feed and seeing if you can get a better signal strength.  
Even if the dish is not perfect on sat, you can still try and peak the LNB, then peak the dish, then peak the LNB and just iterate a few times to get a good clean signal.
## Azimuth Alignment
Now is when the graph starts to come into play. We are first going to look at the graph and find the time when the azimuth is at its peak. We will then go outside with a laptop or computer that can view the waterfall and move the dish side to side and ensure the signal is peaked up left to right. Tip, move the dish right till you just lose the signal, mark it, move it to the left, mark it. Now you know where the azimuth is located for the left (or right) for that part of the orbit. Now wait 12 hours when the satellite is at its right (or left) most and do the same again, move till loss of signal, mark, move the other way till loss, mark and find the middle.   
Now move the dish to the middle of those two master marks.   
Congratulations your dish is now azimuth aligned. Don't lock it down too firm, but well note and roughly fix the dish to the ground at that position.   

## Elevation Alignment
This is the critical one.   
With the dish roughly on signal you need to find a yardstick or stable measurement ruler than can remain in place for a few days to a few weeks. It should be a solid datum point that you can measure the tilt of the dish against. It should not interfere with the movement of the dish at all and should not be in the way of the linear motor that you will be mounting. You should be able to draw on it and thus mark the top and bottom of the orbit in elevation. It can be behind the dish or in front, perpahs at the front rim/lip.   
You will need to be as accurate as possible here. Depending on your look angle to the satellite will determine how much your dish will need to pivot up and down to track the sat.  
It could be as small as an inch (25mm) or up to 3-4 inches (75+mm). Thus you need to be as accurate as possible in your marks. (The angle and movement are based on your location in relation to the satellite - for example, the closer to the equator you are, the more your dish will be looking up - if you live closer to the poles, your dish will be looking more at the horizon.)   
### Find top and bottom of the orbit on the dish   
Over 48 or more hours, look at the graph and pick times when the satellite is at the top and bottom of the orbit.  

This is critical and not optional. Mark the dish position with a marker on your yardstick, note the top of the orbit position and 12ish hours latter, the bottom of the orbit position.  
Once you have these two points clearly and repeatable defined, measure the distance between them.  
Generally it will be around 2 inches (50mm) it can be more, it can be less, but that is roughly the sort of movement we are finding is necessary.   
Now purchase a linear actuator that will cover at least the distance you measured. You can go a little longer, but not much, you don't want to lose resolution.  
Next purchase a 6v DC power supply. The arms are all generally 12v (Some are 24v DC, so be sure and check). At 12v the arm moves WAY too fast, so hence the 6v DC power supply, it still has enough power, but is slow enough to be controlled.  
It is CRITICAL that the actuator is the type that has a position feedback resistor. NOT just end stops, but gives a resistance feedback on the current position.  
Some linear motors only give a pulse output as the motor spins, you *do not* want this type of actuator. ONLY buy the type of motor/arm that has a resistor position indicator. Using this type will show you the position of the arm and thus dish at all times. You will not need to drive the dish 'home' to re-calibrate it, you will always know the exact position of the arm by the resistor value you measure.

Node-RED is outputting the elevation position, we need to remap that to match the position required by the dish.   
The satellite, we know from the graph, moves +-3.2 deg, but what does that translate to on the back of the dish?   
Node-RED has a 'rescale' node, you send it the +-3.2 deg and it rescales it to the resistance of the linear actuator position (say from 2k Ohm to 5k Ohm).
Now you need to link Node-RED to the actuator.   
Here I used an industrial microcontroller, but you could use an Arduino that has a Cat 5 network port.   
Write some code that takes the Node-RED position (Sent every 15 minutes) and compares it with the current resistance value.  
Move the dish via relays in a H-Bridge in the correct direction with a small deadband so that the arm does not hunt continuously around the required setpoint.
Thus every 15 minutes the dish motor will receive a new position from Node-RED and will move the arm to the new location.   
Now, to sync all this up, put the arm on your desk on some paper marked with the length you measured off the yardstick on the dish.  
You now have a mark for the top of the orbit and bottom of the orbit.  
You can simply wait ~12-24 hours watching the actuator on the desk and your graph and make slight adjustments to your microcontroller code and the Node-RED rescale node to ensure the graph to actuator arm match.


Now when it comes time to mount the arm, it's critical that things match up once again.
Pick a time when the sat is at the top or bottom of the orbit.   
Make sure the actuator is at the top or bottom of its stroke.   
Measure the position of the dish independent of the adjustable arm.   
Now cut the arm and mount the arm. Make sure the arm is very securely mounted to the dish, but can still pivot as the dish moves up and down. Grabbing the top of the dish and moving it up and down should have very little slop.   
In 15 minutes time, your dish will be tracking the satellite very accurately.


<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>