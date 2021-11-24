# Ins and outs of Jaero.   
   
Navigation: [home](README.md)  

The core of this whole project is the software called Jaero.  
This page will grow over time. Check back now and then.  
## Jaero on Windows   
Use the November 1.0.4.13 dirty version, you don't need to install it, just run it from the directory you unzip it from. This version fixes a lot things and most importantly it uses the latest libacars-2 version which itself has a lot of updates and bug fixes. It also allows you to use BaseStation.sqb for its logging aircraft database lookup. The 1.0.4.13 of Jaero adds the ZMQ input for data. You should be using at lest this version. There is a how-to page for setting up SDRReceiver on Windows [here](SDRReceiver.md)   
    
basestation.sqb. This is a pseudo 'standard' of aircraft details database. As Jaero decodes aircraft messages, it looks up each ICAO (Jaero calls them AES) in the database and provides type and owner information in its log file. If you are going to use Node-RED to track the aircraft, skip this step.   
The basestation.sqb file that this version of Jaero includes has around 188,000 aircraft details, but we can quickly do better.    
Visit the flightairmap page and download their basestation.sqb file: <https://data.flightairmap.com/>  
The link is at the bottom of that page.   
Unzip it on your computer and copy the file to your Jaero subdirectory and replace (over write) the one in there. The flightairmap database has 380,000 aircraft, so almost double the chances of Jaero showing the information for any satcom ACARS messages you decode.   
If you are using Node-RED I will walk you through building an even larger database with around 558,000 aircraft details. Or you can get creative and modify your own database to use with Jaero.    
    
Once you have copied the database over, you can now double click Jaero.exe and run it.   
But lets just do one more tweak for those of you running standalone (ie, no Node-RED) and want to see some aircraft logs/details.   

### Jaero Log Link   
Click on the gear icon, then click on the second tab in the settings, the 'Log Window'.   
Here you will see the link that will be opened in your web browser when you click on the aircraft drawing in the Jaero log.   
Out of the box it is set to: `http://www.flightradar24.com/data/airplanes/{REG}`  
This is Ok for some people, but many would rather it open to ADSBExcahnge, good news, we can change it.    
Delete the fightradar24 link and replace it with: `https://globe.adsbexchange.com/?icao={AES}`   
Now when you click on that drawing (and first highlighting the aircraft of interest in the Jaero log list), you will open that aircraft last known position on the ADSBExchange map.   
If you are going to be using Node-RED, I will show you how to make those links in a function node so we can skip this step.


<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>