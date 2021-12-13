# Using Node-RED to manage ADSC, ADSB, ACARS, VDL2, HF-DL and other aircraft type messages.

Navigation: [Jaero](jaero.md) : [SDRReceiver](SDRReceiver.md) : [Inmarsat](Inmarsat.md) : [L-Band](L-Band.md) : [autoTLE](autoTLE.md) : [OpenSkyAPI](OpenSkyAPI.md) : [VRS](vrs.md) : [MQTT](mqtt.md) : [VHF-VDL2](vhf-vdl2.md) : [Raspberry Pi](raspberrypi.md): [Telegram Chat Bot](telegram.md) : [DragonOS](DragonOS.md)

**Node-RED Dashboard - The main website**  

Live ACARS, VDL, HFDL and Inmarsat C-Band and L-Band messages for most of the planet - broken down into different bands and types of aircraft's (like Bizjets and Military).  
<a href="http://thebaldgeek.net:2277/ui/#/0" rel="noopener" target="_blank">http://thebaldgeek.net:2277/ui/#/0</a>   

Take your time on that 'site'. The menu is on the top left (the three bars).  
View each of the pages and *pay attention to the update log page at the very bottom of the page menu.* This is the best (and only?) way of finding out any new features that has been added.  
I am constantly working on the site. The site is a case of function over form. It is not really 'friendly', but it is rather powerful.
For example, you can filter on commercial or military CPDLC messages, or ACARS messages in general. 

**Planes on a map**   

If you want to look look at just the aircraft that we are tracking via satellite: <a href="http://thebaldgeek.net:99/tar1090/" rel="noopener" target="_blank">http://thebaldgeek.net:99/tar1090/</a>   
If you want to see aircraft that currently have ACARS messages associated with them:
<a href="http://thebaldgeek.net:22234/" rel="noopener" target="_blank">http://thebaldgeek.net:22234</a> (This map uses the fantastic work of Fred and [ACARShub](https://github.com/fredclausen/docker-acarshub))   

If you want to get a feel for the satellite coverage over the past 24 hours (it's memory heavy so zoom and pan slowly): <a href="http://thebaldgeek.net:99/tar1090/?pTracks" rel="noopener" target="_blank">http://thebaldgeek.net:99/tar1090/?pTracks</a>  
If you want both ADSB and ADSC planes on a map: <a href="http://thebaldgeek.net:99/recombine/" rel="noopener" target="_blank">http://thebaldgeek.net:99/recombine/</a>  

**Data Graphs**  
If you want to see the data rates for the ADSC aircraft the system tracks: <a href="http://thebaldgeek.net:99/graphs1090/" rel="noopener" target="_blank">http://thebaldgeek.net:99/graphs1090/</a>  
  
## About ## 
The Node-RED dashboard site is fed from Inmarsat 98W (4F3), 54W (3F5), 143E (4F1) and 25E (AF1).  
There are a few people that generously send their data from different parts of the globe (Asia Pacific, the Americas and UK).  
An ADSC feed from the UK (Alphasat) is in the works, the dish tracking is still being setup. Data is feed for some of the orbit. L-Band ACARS from Alphasat comes from a few feeds and is fairly consistent.  
L-Band ACARS feeds from the other three satellites is very consistent.  
While all of us work together to keep our data feeds up and running 24*7 we are all just aviation enthusiasts with families and day jobs, keep that in mind as you view the data.  
If you have an ADSC satellite dish setup and would like to feed your data to the site, please let me know.

###  READ THIS!

My motto is 'fail fast, fail often'. I am NOT a programer. Do NOT use any of the code shown here. These pages and the code on them are for entertainment use only.   
The best way to put this is: `I don't know what I'm doing, but I know that I don't know what I'm doing.`  
The pages on this site are a brain dump. There are a lot of different moving parts to running an effective ground station. Many different people and web sites have small snippets of information about putting together a satcom ground station. Some people don't share any details at all and leave it to us to relearn what they don't share.  
This site is an attempt to pull this together and document all the required steps and parts needed.

### Support or Contact

I will do my best to support your Node-RED aircraft spotting / tracking adventures, but please keep in mind, I am NOT a programmer. I honestly have no idea or right to be doing any of this, so your milage may vary. Also, since I am not a programmer (Have I mentioned I am not a programmer?), I have no idea what a 'pull request' is or how to deal with one, so if you raise one... yeah, sorry... I can't help.

Check back often, this site is being updated almost daily.
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>