# msg by msg break down of interesting ACARS exchanges over a specific flight.   
   
Navigation: [home](README.md)  
   
     
ADSB/C is the where   
ACARS is the why

When you combine the two systems, you end up with a much more accurate telling of the flight.  
On this page thebaldgeek breaks down one (soon two) such flight to show how ACARS explains why ADSB/C folks saw the return, but claimed they did not know why (FlightRadar24, FlightAware (and others) social media teams have done this more than a handful of times - if they can miss ACARS, others might as well).   
  
### QF63 RTB (return to base) flight due to maintance issue. (tbg suspects engine issue)   
Dec 25th 2024.   
  
thebaldgeek comments in lowercase, ACARS in upper.
   
Note that a lot of system pings and ACARS that TBG does not fully understand are skipped over.    
There are around 300 ACARS from this part of the flight, so we are just looking at a human high level overview to give a feel for how ACARS can, in real time, fill out the details of the flight.     

We pick up the flight as they passed the last VHF ACARS receiver over Tasmania and the aircraft switched to satcom.
  
```
"time": "2024-12-25T00:35:50.033Z",  
"sat": "C-143E",  
MEDIA ADVISORY, VERSION 0:  
LINK VHF ACARS LOST AT 00:35:43 UTC  
AVAILABLE LINKS: DEFAULT SATCOM  
```
    
tbgmap.airframes.io is the only tar1090 ADSC site around, so it shows tracking beyond Tasmania, ie ADSB range.
The links should take you to the map at the time they are sent.  
  
  
At this timestamp, everything is on track and they get sent arrival overview information from the ground (Note the satcom source is L-Band, that is uplink to the aircraft) and are asked to confirm the ATIS (Air Traffic Information System) sent to the aircrew.  
```  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T00:52:28.366Z",  
[tbgmap.airframes.io](https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735087948)  
VH-OQG JNBATYA.TI2/FAOR ATIS P 0001Z. EXP ZONE IMC ARR RWY03L DEP RWY03L CLEARANCE DELIVERY ON 121. 9  
TRL FL090 WIND 030/9KTS VIS ABV 10KM SCT 600FT BKN 1400FT T16 DP15 QNH 1026HPA TEMPO VIS3000M BCFG  
CONFIRM ATIS  
```  
Here is the first sign of the situation unfolding.  
The aircraft via C-Band (from cockpit to ground) request weather reports for - of all places - the airstrip in Antarctica!   
tbg can not explain this one at all!  
```  
"sat": "C-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T01:15:36.068Z",  
[tbgmap.airframes.io](https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735089336)  
VH-OQG FLIGHT QF63  
U22AQF0063  
WX REQUEST  
QFA0063/25  
ACTUAL  
FAOR NZFX NZWD  
```  
  
Dispatch sends back some data (again, via L-Band. Last time tbg is going to point this out, you get the idea of the flow of satcom by now?).  
```  
"icao": "7C4926",  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T01:15:41.335Z",  
[tbgmap.airframes.io](https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735089341)  
VH-OQG .HDQONQF ~6 01:15 ACTUAL  
METAR TTF FAOR 250100Z 03009KT 9999 BKN005 OVC013 16/15 Q1026 NOSIG=  
AIRPORT DATA MISSING: NZWD  
MISSING WEATHER FOR AIRPORT FOR NZFX  
```  
Standard automated position reports are still sent by the system.  
These are of interest and can be plotted.  
Point being, not all L and C band messages are from humans.  
```  
"sat": "C-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T01:39:27.113Z",  
[tbgmap.airframes.io](https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735090767)  
VH-OQG FLIGHT QF63  
J43AQF0063/MELCAYA.ADS.VH-OQG  
BASIC_REPORT:  
LAT = -48.5228 LONG = 140.781 ALT = 34004 FEET. TIME PAST THE HOUR = 39M 18S FOM = 1D  
TRUE TRACK = 207 DEG. GROUND SPEED = 451 KNOTS. VERTICAL RATE = -16 FPM.  
WIND SPEED = 108 KNOTS. TRUE WIND DIRECTION = 281 DEG. TEMPERATURE = -48.5 DEG C.  
NEXT WAYPOINT LAT = -48.7999 LONG = 140.567 ALT = 33996 FEET. ETA = 00:02:38  
```  
Crew clearly are working the situation and now request weather data for YPPH (Perth Australia)  
Why so far? They need a good sized airport to land an A388, they need to house a lot of passengers, they need QANTAS maintenance facilities (if possible) and most of all, they need time to burn off fuel and get their landing weight down - more ACARS about this at the end.  
```  
"icao": "7C4926",  
"sat": "C-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T03:14:36.892Z",  
[tbgmap.airframes.io](https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735096477)  
VH-OQG FLIGHT QF63  
U36AQF0063  
WX REQUEST  
QFA0063/25  
ACTUAL FOR YPPH FIMP  
```  
Dispatch operators are the unsung heroes of the skies… 10 seconds later they send the METAR report.  
  
```  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T03:14:46.534Z",  
[tbgmap.airframes.io](https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735096487)  
VH-OQG.HDQONQF ~6  
03:14 ACTUAL METAR TTF FAOR 250300Z 07010KT 9000 OVC006 16/14 Q1026 NOSIG=  
METAR YPPH 250300Z 20016KT CAVOK 24/06 Q1016  
RMK RF00.0/000.0=  
SPECI YPPH 250237Z 20015G26KT CAVOK 23/06 Q1016  
RMK RF00.0/000.0=  
METAR FIMP 250300Z 08010KT 9999 FEW018 27/21 Q1016  
```  
There are of course voice comm’s going on. A topic for another time.  
Here we see plans change and we now have dispatch send weather for Melbourne, Adelaide and Perth  
```  
"icao": "7C4926",  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T03:43:56.319Z",  
[tbgmap.airframes.io](https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735098236)  
VH-OQG  
HDQONQF ~6 03:43   
ATIS YMML P   250329  
APCH: EXP GLS OR ILS APCH  
RWY: WND: 030-160/8. MAX TW 5 KTS WX: CAVOK TMP: 32 QNH: 1012  
-----END OF MESSAGE-----  
ATIS YPAD C   250323  
RWY: 23   WND: 260-320/10. MAX TW 3. MAX XW 15. WX: CAVOK\n\t   TMP: 33  
QNH: 1008  
-----END OF MESSAGE-----  
ATIS YPPH X   250310  
APCH: EXP ILS APCH  RWY: 21 AND 24 FOR ARR. RWY 21 FOR DEP.   WND: 200/15 MAX XW 12 KTS, RWY 24  WX: CAVOK  TMP: 24+ QNH: 1015  
-----END OF MESSAGE-----  
```  
Dispatch reaching out and checking if the crew need anything.  
Sometimes this sort of check in happens when dispatch operators switch over due to breaks or end of shifts.  
```  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T04:37:58.713Z",  
[tbgmap.airframes.io](https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735101479)  
VH-OQG \tQFFLTDISP~1   
GDAY 63  
DO U REQUIRE ANYTHING FROM  
FLT DISPATCH  
LET ME KNOW IF U DO.  
REGARDS ANDY  
FLT DISPATCH  
```  
  
Dispatch letting the crew know the game plan so they can keep the passengers in the loop.  
```  
"icao": "7C4926",  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T06:14:52.760Z",  
[tbgmap.airframes.io](https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735107293)   
VH-OQG \tQFOPSCNTL~1  
QF63 THE CURRENT PLAN IS FOR AN 0700LT  
DEPARTURE TOMORROW ON A DIFFERENT  
AIRCRAFT. ENGINEERING ARE CURRENTLY  
REVIEWING. DUE TO SHIFT HANDOVER, HAVE  
BEEN ADVISED THERE WILL NOT BE AN ANSWER  
UNTIL 1830LT AT THE EARLIEST.  
OPS CTL"  

"icao": "7C4926",  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T06:27:21.766Z",  
[tbgmap.airframes.io](https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735108042)  
VH-OQG \tQUSYDKOQF~  
HI PARK BAY: 10  
BAGGAGE CAROUSEL: 15  
A-C OPS 63 JNB 0700+  
FOR THE CSM: ALL PASSENGERS WILL NEED TO FILL IN AN AUSTRALIAN ARRIVAL FORM BEFORE DISEMBARKING.  
WE WILL ADVISE SOON ON ACCOMMODATION DETAILS  
THANKS, QANTAS SYDNEY  
```  
This is a ‘fun’ one that tbg does not have an answer to…  
From the flight crew to maintenance that they are going to land a little on the heavy side.  
```  
"sat": "C-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T07:25:40.601Z",  
[tbgmap.airframes.io](https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735111541)  
VH-OQG FLIGHT QF63  
U24AQF0063  
TO ENGINEERING  
MAINT QF63 ANTICIPATED LW IS 421000KG. APPROX 30T ABOVE MLW   
```  
  
-------------------------- EOL --------------------------------
  
Check back now and then for updates to this page.     
    
# ------------------ Midway ------------------------------------  
NOTE: Dec 27 2024. tbg added this flight from his personal blog.   
Keep in mind that this happen mid 2021. It was before the website went viral during the Afganistan Extraction, before the sale of ADSBExchange, before thebaldgeek.github.io. back when the site only had 12 hours of search history.  
Posting the blog post here largly unedited so you can hear thebaldgeeks excitment and passion for satcom ACARS back in the day. There will be errors since tbg and others have learned a TON since then, have not edited or corrected any of those errors.      
Lastly, in March 22nd 2024 all the photos / images / screenshots from this flight were lost. The text below has been copied from the wayback machine / web.archive.org. Had they not grabed it it would have been lost as well.   
tbg will keep an eye out for any images and add them when / if he finds them on old hard drives and will update this flight of interest.   
Ok, all that said as backstory.... Let's jump in, its a great story.       
     

### UA2781 lands at Midway Atoll on April 16th 2021   

Settle in, this is going to be a long one.   

Background. Oh so briefly.   

C-Band uses a 6 foot (2 meter) satellite tracking dish on ~3.4 GHz. It picks up the aircraft to ground crew communications.   
L-Band uses a 7 turn 3D printed helix (swapped out from a flaked out patch antenna only 3 days before this went down) on ~1.5 GHz. It picks up the dispatch (ground) to aircraft communications.   
  
What unfolds is a testament to having a fully configured and well tuned Satcom/AERO ground station. Full credit to my mate in Australia. Andrew runs the station and keeps it tip top. (Even to the point of drilling a hole in the dish to let the water drain out when it tropical pours rain!)  
As well as needing a reliable RF data source, to see something unfold in real time and share it with aviation geeks around the world, you need a real time web-based dashboard with some sort of way to string together the conversation (aka, a database).  
  
Over the years I have been finding ‘interesting’ ways to filter and then be alerted to ACARS messages that are out of the routine. The result is a bit of JavaScript that has a list of carefully curated words, if any are in an ACARS message from any source, I get notified, exactly how depends on the ‘severity’ of the trigger word.  
  
Ok, enough backstory.  
  
Messages are going to be tagged as follows:  
‘Pilot’. This is Pilot to dispatch. They come via the dish.  
‘Dispatch’. This (in this case) is the United Airlines dispatch operator. They come via the helix.  
‘Aircraft’. This is the aircraft avionics (software). They come in via the dish.  
Names and other personal details have been redacted. (Captin Walt, if you find this, please drop me a line – I’d love to chat).  

April 16th I was minding my business when this message set the adventure in motion.  
```
Pilot: A254D8: 01:22:14 17-04-21 AES:A254D8 GES:50 2 .N24974 ! 5Z 2 Flight UA2781 M98AUA2781/DM FODM MSG / PGUM  
PMDY 16 152212 ROBERTA WOULD U PLZ CALL MY WIFE xxxxx AND LET HER KNOW WE ARE OK…xxxx THE OTHER 2 PILOTS  
WILL TRY LATER TODAY THANKS.  
```
This got my attention of course. It is very much of out of mundane.  
Worth a little look right?  
  
  
  
At first glance it looks ok?  
You sometimes see funky numbers in the panel on the left, so the altitude did not set me off.  
Before I could push it from my mind….. Just a few minutes latter, I saw this:  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA P QUDPCULUA-1MSG FROM WHQDM UA2781/16 PGUM PMDY SENT: 13:50:54Z   
HELLO UA2781, I SEE YOU ARE ON THE GROUND. PLS CALL FODM WHEN ABLE DCAFO  
```
Ok, so now I am really interested.  
Lets zoom in a bit…  
  
  
  
Right. There is no way they intended to land there!   
Now I am really intrigued and started to put the word out to a few mates. I did not tweet it as I knew it would be complicated, but still let a few avgeeks know on Discord/Messenger/Email etc.  
```
Pilot: GES:50 2 .N24974 ! 5Z 7 Flight UA2781 M96AUA2781/C4 DISP MSG / PGUM PMDY 16 142733 SEND FORM VIA  
 ACARS NO CELL OR WIFI  
```
Sounds like the crew is getting sorted, using the aircraft satcom ACARS system to talk back and forth to / from dispatch!! Pretty crazy cool.  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA M QUWHQVDUA?1MSG FROM DISP UA2781-16 PGUM PMDY YOUR CLEARANCE  
WAS CANCELLED WITH OAKLAND, AND WE ARE STILL TRYING TO CONTACT ANYONE ON THE ISLAND, ALTHOUGH I SUSPECT THAT   
SOMEONE WOKE UP WHEN A 787 LANDED. PLEASE LET ME KNOW IF/WHEN YOU GET IN CONTACT WITH ANYONE ON THE GROUND  
```

Not sure how long ADSBx holds the history, but this what we were looking at:  
[adsbex](https://globe.adsbexchange.com/?icao=a254d8&lat=26.824&lon=177.129&zoom=6.0&showTrace=2021-04-16)  
  
Midway Atoll is an emergency diversion point for ETOPS operations, so it makes sense they went there if there was an issue.  
It looks like they just followed procedure and flew straight in.  
  
We later read a media report that said they flew around the island a few times before landing, but we have no ACARS or ADSC data to confirm that.  
It also does not make sense to extend an emergency like that.  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA W QUNDCULUA~1MSG FROM TOMC CAPT – WE ARE STILL WORKING ON   
RECOVERY PLAN AND WILL SHARE WITH YOU ONCE WE HAVE THE DETAILS. COULD YOU SEND YOUR FOB AND THE  
CURRENT AC LOCATION. ALSO, HAVE YOU HAD ANY CONTACT FROM ANYONE ON THE FIELD YET. THANKS  
```
  
FOB is Fuel On Board. Its a common way to ask or report how much gas is in the tank. (Sent in weight, either lb or kg or something else, depending on the aircraft owner, crew and region – yay for standards right?).  

```
Dispatch: GES:50 2 .N24974 ! 5Z 8 Flight UA2781 M97AUA2781/C5 TOMC MSG / PGUM PMDY 16 151158 CAN U   
EMAIL THE CAPT THE COMPLETED FUMES FORM THNX UNITED.C OM  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA M QUDPCULUA.1MSG FROM TOMC UAL2781-16 PMDY KLAX CAPT –   
TOMC WORKING ON GETTING SUPPORT FOR YOU. I NEED TO SEND YOU SMOKE/ODOR FORM FOR YOU TO FILL OUT AND  
EMAIL BACK TO ME. CAN YOU SEND EMAIL OR CALL TOMC SO WE CAN GET THIS TAKEN CARE OF. THANKS  
```
Ok, so from that we know they landed due to smoke somewhere in the aircraft. Probably the cockpit since the pilot/FO had to smell it. (Remember, it was a cargo flight).  
  
At this point I am just so stoked that the Inmarsat 143E (Cairns Australia) ground station is working so well at this stage.  
Times like this makes me feel it was all worth it.  
The crazy thing is I sent Andrew a 3D printed 7 turn helix my son printed and I built to replace his SDR-Blog Patch antenna (which was not great), Andrew just got it installed about 3 days prior and its working great.  
We are getting both sides of the conversion live!!!!  
Very excited!  
I missed this one in the timeline while was checking out other stuff….  

```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! AA H /OAKODYA.AT1.N2497425B581AA4E284D8965041895A4D38B  
4D0549116CA0870674E9F51041870E2D0A8820A084DDC375CB97499A82BCFA52E4CE8E827CE4126A009901 FANS-1/A   
CPDLC Message: CPDLC Uplink Message: Header: Msg ID: 11 Timestamp: 13:24:06 Message data:   
[freetext] PMDY ADVISES THEY CANNOT ACCEPT A B787…IM WORKING ON IT  
```
   
CPDLC is “CPDLC is a two-way data-link system by which controllers can transmit non urgent ‘strategic messages to an aircraft as an alternative to voice communications. The message is displayed on a flight deck visual display. The CPDLC application provides air-ground data communication for the ATC service.”  
They are so important and often interesting we filter them out and display them in their own table on the website.  
In this case dispatch are telling the pilot that they knew the aircraft was in distress and Midland was the best option. Dispatch is ahead of the flight (so to speak) and are trying to raise anyone on the island to ready things for the landing.  
  
Aircraft: While its sitting on the ground sends out automated messages from time to time.  
  
```
GES:50 2 .N24974 ! H1 5 Flight UA2781 506IUA2781#T5BG00C00C00000003Q04504U05R02H01H01301931BO  
1641020630CK0000CN0UF1641590EG60E0C::::::::::::::::::::::1)))0V700N00M00000707)  
```
  
Its a bit cryptic, and many of us are working on their exact meaning. Usually its stuff like engine or aircraft health and status data.  
  
A few of the guys were looking at background information while I was mashing the ‘refresh’ button on the data feed.  
  
  
The runway is nice and long. A few guys were looking up the runway length needed for the aircraft and its rough cargo weight.  
No problems there.   
The birds on the other hand…..  
  
The aircraft is still spewing out automated messages like this one:  
  
```
AES:A254D8 GES:50 2 .N24974 ! RA Q QUNDCULUA~1LTD ADVISORY UA2781/16 PGUM PMDY SENT: 17:24:00Z  
*LENGTHY TARMAC DELAY* THE LTD CLOCK HAS BEEN EXCEEDED. *********************** DIVERSION LTD  
MUST BE MANAGED BY NOC. LTD BEGINS AT ON AND ENDS AT EGRESS OR OFF. AUTOMATED MESSAGES DO NOT  
ALWAYS HAVE ACCURATE TIMES *********************** PILOT ACTIONS: PROCEED TO GATE OR EGRESS   
POINT IMMEDIATELY. NOTIFY DISPATCH/CABIN AND PAX OF STATUS AS REQUIRED. *MANDATORY IOR*  
```
  
This is a result of:  
“47 passengers spent almost six hours — longer than it usually takes to fly across the continental U.S. — sitting onboard a plane that was parked on the tarmac of Rochester International Airport in Minnesota.”  
Airlines that defy the tarmac delay rules can be fined up to $27,500 for each passenger on board the affected flight. With commercial jets routinely carrying over 200 passengers these days, that means failure to follow the tarmac delay rules could cost an airline more than $5 million in fines for a single flight. The potential for that kind of financial hit is probably enough to get the attention of even the largest airline.  
  
So, the aircraft has this tarmac delay built in and messages the pilots that they need to take action and keep track of the time they are on the ground.  
Even though this is a cargo flight, the aircraft share similar software regardless of their ‘cargo’, be it boxes or people.  
  
Back to the story.  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA S QUNDCULUA~1MSG FROM DISP UA2781-16 PGUM PMDY MDY  
IS IN CONTACT WITH YOU NOW?  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA J QUNDCULUA~1MSG FROM TOMC CAPT – REGARDING THE  
GPU – I SUSPECT THE AC HAS PLENTY OF FUEL FOR THE APU AND BASED ON NOT KNOW THE CONDITION/  
RELIABILITY OF THE GPU, LET’S NOT USE IT AND KEEP ON THE APU PLEASE  
```
  
APU, aircraft power unit. GPU, ground power unit. The aircraft has to be kept powered up (unless going into long term cold storage – ie, not in this case). Dispatch are saying they don’t know if Midland has the gear to keep the aircraft powered, they know the onboard power unit can do it, so use that one.  
  
```
Pilot: GES:50 2 .N24974 ! 5Z 7 Flight UA2781 M14AUA2781/C5 TOMC MSG / —- —- — 174628 ROGER. APU ONLY  
```
  
They are going to use the on board aircraft power unit as its a known entity.  
Pretty cool to see the Pilot acknoladge messages from dispatch in real time via satellite from half a planet away.  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA N QUNDCULUA~1MSG FROM TOMC THANKS – COUPLE ITEMS –   
COULD YOU GIVE ME FUEL ON BOARD DETAIL AND WHERE IS THE AC PARKED, ARE WE GOING TO NEED A TOW BAR? THANKS  
```
  
After years of reading ACARS messages I personally love the guys in dispatch almost as much as pilots now. They work so hard for the crew (and passengers). This operator is thinking way ahead and wants to be sure they have everything the crew will need to get back in the air before they even need it. A good dispatch operator will reduce the crew work load a lot (I have also seen a fair few snarky dispatch messages FWIW).  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA T QUNDCULUA~1MSG FROM TOMC CAPT – ANOTHER QUESTION   
CAME UP THIS MORNING AND IT’S A LONG SHOT – BY CHANCE, IS IT POSSIBLE THERE WAS A BAG/CONTAINER   
OF “MINI NORI MAKI”; RICE CRACKERS IN THE FLIGHT DECK?  
```

Wait. What?  
A packet of crackers? A very specific type of crackers?     
This cracked a few of us up.  
[The crackers in question](https://www.snackhawaii.com/products/enjoy-mini-nori-maki-4-oz)  
Its a real thing, but still… bit odd for dispatch to ask the crew?  
  
```
Pilot: GES:50 2 .N24974 ! 5Z 6 M15AUA0000/C5 TOMC MSG / —- —- — 175821 FOB…70.5 PARKED NEAR LARGEST 
BUILDING ON AIRPORT NO TOW BAR REQUIRED PLENTY OF ROOM TO TAXI OUT  
  
Displatch: AES:A254D8 GES:50 2 .N24974 ! RA W QUNDCULUA~1MSG FROM TOMC EXCELLENT! THANKS – ARE YOU   
ALL STILL STUCK ON BOARD OR DO YOU HAVE ACCESS TO THE RAMP YET?  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA Y QUNDCULUA~1MSG FROM TOMC IF YOU ARE ABLE AND WILLING,   
IT WOULD BE GOOD TO HAVE A WALK AROUND THE AC TO MAKE SURE NO BIRD STRIKES INBOUND TO MDY AND CONDITION   
OF THE TIRES. IF WE NEED TIRES, WILL NEED TO TAKE THAT INTO ACCOUNT FOR THE CHARTER OR RESCUE FLT TO  
CARRY YOUR WAY. THANKS  
```
  
Again with dispatch looking ahead and working the situation.  
Also not the first time the ‘bird’ word will come into play on this adventure.  
  
```
Pilot: GES:50 2 .N24974 ! 5Z 2 M16AUA0000/C5 TOMC MSG / —- —- — 180846 NO CRACKERS. YES WE HAVE A   
LOADING BRIDGE. TIRES ARE FINE  
```
  
Ooookkkk, so the pilot checked the tires (for a short landing, the brakes and tires might have been heavily used and also a somewhat unmaintained airstrip might have hand some FOD (foreign object debris) and the cockpit for crackers….  
  
```
Displatch: AES:A254D8 GES:50 2 .N24974 ! RA G QUNDCULUA~1MSG FROM TOMC ALL GOOD NEWS – THANKS!   
APPARENTLY, THERE HAS BEEN HISTORY OF THESE TYPE CRACKERS GENERATING A HOT ELECTRICAL SMELL IN   
CONFINED SPACES AND HAVE CAUSED DIVERTS IN THE PAST. WHO KNEW! GLAD TO HEAR YOUR ABLE TO STRETCH   
YOUR LEGS. IF YOU ALL ARE GOING TO BE LEAVING THE AC, WE WILL NEED TO ADDRESS SHUTTING IT DOWN IF   
THIS HAPPENS BEFORE WE HAVE SOMEONE ELSE TO MONITOR IT. THANKS  
```
  
Crackers that smell like smoke!!!  
Bahahahah  
That’s just amazing. Those crackers have caused diverts in the past?! The stuff you learn via ACARS. Just awsome!  
  
```
Pilot: GES:50 2 .N24974 ! 5Z 0 M17AUA0000/C5 TOMC MSG / —- —- — 182343 PREFLIGHT SHOWS NO CONCERNS   
TIRES ARE FINE AND BRAKE TEMPS NEVER EXCEEDED NORMAL RANGE  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA N QUDPCULUA.1MSG FROM TOMC UAL2781-16 PMDY KLAX   
THANKS xxxxx! DO YOU KNOW WHAT FLT OPS IS PLANNING FOR YOU YET? WWHQ093E  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA S QUDPCULUA.1MSG FROM TOMC UAL2781-16 PMDY KLAX CAPT –   
ARE YOU ALL STILL ON THE AC WWHQ093E  
```
  
At this point I had be following along for more than a few hours and was pretty tired.  
The nice thing is that Node-RED is putting the ACARS messages into a MySQL database on a 12 rolling buffer so I could just catch up in the morning. (A few of my other-side-of-the-planet avgeek buddies kept watch).  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! C1 G .DPCULUA 171434 AGM AN .N24974 – UA2781/17 PMDY PHNL   
SENT: 14:34:17Z PLEASE CONFIRM BEFORE DEPARTURE: -TOTAL SOULS ONBOARD -CARGO IN THE PITS? YES OR NO   
-GALLEY OPTION 1,2,3,4 OR 5 1. CREW MEALS IN FC GALLEY, ALL OTHER GALLEY CARTS INSTALLED BUT EMPTY 2.   
ALL GALLEY CARTS ONBOARD INCLUDING CONTENTS FOR RETURN PASSENGER FLT 3. ALL GALLEY CARTS INSTALLED BUT   
EMPTY 4. NO GALLEY CARTS INSTALLED 5. CREW MEALS IN FC GALLEY, NO OTHER GALLEY CARTS INSTALLED REPLY UA   
COMM>LOAD PLANNING OR MISC LP OPBLP  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA I QUDPCULUA-1MSG FROM OPBLP UA2781/17 PMDY PHNL SENT:   
14:37:09Z HELLO FROM CHICAGO . IF U PLZ MX WILL BE . LOADING AOG AND TOOLS. THEY BROUGHT W THEM.   
PLZ VERIFY IT WILL B . SAME WGHT AND IN THE . BULK PIT. . . QUESTIONS – CONTACT LOAD PLANNER OPBLP  
```
  
Right, it seems while we slept a maintenance flight arrived from Hawaii with some crew and gear.  
We did not check out Satcom ACARS for them – in hindsight I will the next time something like this happens.  
  
```
Dispatch: (We got a few of these releases, so are only posting the one here)  
AES:A254D8 GES:50 2 .N24974 ! RA Z QUHDQWDUA?1DISPATCH RELEASE UA2781/17 PMDY PHNL SENT: 15:02:08Z DISPATCH  
RELEASE UAL2781(2781) – 17APR21 PMDY/MDY PHNL/HNL N24974/3974 B789 ———————– RLS 1 FFD AFFIRMATION:   
PO EMP NAME EMP NO FFD — ———- —— — CA HE GAINES 136588 NO FO AW ADAM 250443 NO ———————— RELEASED IFR   
TO PHNL CHI55 DEPARTURE ALTN: N/A DESTINATION ALTN: PHJR/JRF 120 ETOPS ENROUTE ALTERNATES: EA:PMDY-PHNL   
MIN T/O FUEL:36685 THE CAPTAIN AND DISPATCHER NAMES ON THIS RELEASE CONSTITUTES THE REQUIRED SIGNATURES   
PER 121.663 AND INDICATES THE PILOT  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA A QUDPCULUA-1EPNF INFO UA2781/17 PMDY PHNL SENT: 15:02:09Z   
NO DANGEROUS GOODS PLANNED  
```
  
Ok looking at that message, we see PMDY (Midlands Atoll) and PHNL (Daniel K. Inouye International Airport, aka Honolulu International Airport). So we know they are going to do a short hop between islands on this flight. Probably to get more fuel in PHNL to finish their original flight to KLAX.  
  
```
Aircraft: GES:50 2 .N24974 ! 23 9 Flight UA2781 M26AUA2781/23 CDOORS CLSD / PMDY PHNL 17 150347/TIME   
1745 /LOC +28.2097,-177.3793  
  
Pilot: GES:50 2 .N24974 ! 5Z 6 Flight UA2781 M29AUA2781/LP LOAD MSG / PMDY PHNL 17 151303 9 SOB YES   
CARGO GALLET OPT 1  
```
  
SOB is soles on board.  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA Z QUDPCULUA-1MSG FROM OPBLP UA2781/17 PMDY PHNL SENT:   
15:17:47Z COPY 9 SOB 2 IN CKPIT. 7 IN FIRST…IS THAT . CORRECT? . . . . . . QUESTIONS – CONTACT   
LOAD PLANNER OPBLP  
```
  
The load planer needs to know how the weight is spread out on the aircraft.  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA A QUWHQVDUA?1MSG FROM DISP UA2781-17 PMDY PHNL   
HI ANY ETD YET? THANKS  
```
  
Usually dispatch work with the local ATC, but there is none on Midway Atoll.  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA B QUWHQVDUA?1MSG FROM DISP UA2781-17 PMDY PHNL DID  
THE 737 TAKEOFF YET?????  
```
  
United ground support are wondering if the flight that had the maintenance guys on board has cleared the island yet.  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA D QUDPCULUA-1MSG FROM OPBLP UA2781/17 PMDY PHNL SENT:   
15:20:37Z PLZ VERIFY MX HAS . LOADED AN ADDITIONAL . 750 PDS IN BULK. AOG. AND TOOLS THEY BROUGHT   
FROM HNL ON THE . NARROW BODY . . . QUESTIONS – CONTACT LOAD PLANNER  
  
Pilot: GES:50 2 .N24974 ! 5Z 4 Flight UA2781 M30AUA2781/LP LOAD MSG / PMDY PHNL 17 152312 AFFIRM ALL IN 1ST  
  
Pilot: GES:50 2 .N24974 ! 5Z 5 Flight UA2781 M31AUA2781/C4 DISP MSG / PMDY PHNL 17 152432 ETD 1545 737 HAS LEFT  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA H QUWHQVDUA?1MSG FROM DISP UA2781-17 PMDY PHNL THX CHIDD SWED  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA I QUWHQVDUA?1MSG FROM DISP UA2781-17 PMDY PHNL CAN U PLZ LET   
LP KNOW THE 750 LBS TOOLS PARTS VERIFIED ON BOARD??? THX  
  
Pilot: GES:50 2 .N24974 ! 5Z 8 Flight UA2781 M32AUA2781/C4 DISP MSG / PMDY PHNL 17 153309 APPARENTLY WE   
CANT MAKE OUR WHEEELS UP TIME. MX STILL WORKING ON THE MEL ITEMS. THEY WORKING W/ TOMC  
```
  
MEL is Minumin Equipment List. ie the stuff that really really matters to fly.  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA K QUWHQVDUA?1MSG FROM DISP UA2781-17 PMDY PHNL RGR THAT AND   
NO CURFEW EXTENTION RIGHT?  
```
  
The crew cant fly without rest. So dispatch always keep track of pilot flight hours and remind the crew when they need to rotate.  
  
```
Pilot: GES:50 2 .N24974 ! 5Z 1 Flight UA2781 M33AUA2781/C4 DISP MSG / PMDY PHNL 17 155204 300 POUNDS OF   
MX GEAR NOT 750 FWIW  
  
Pilot: GES:50 2 .N24974 ! 5Z 4 Flight UA2781 M34AUA2781/C4 DISP MSG / PMDY PHNL 17 155726 NO EXTENSION   
YOU WOULDNT WANT ONE B/C THESE BIRDS START SWAR MING LIKE CRAZY BUT WANTED LP TO HAVE MX GEAR WT.  
LETS GO TONIGHT    
```
  
Ah, the birds….  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! C1 R .DPCULUA 171558 AGM AN .N24974 – /UA2781/17 PMDY PHNL SENT:   
15:58:06Z CAP GAINES PLZ BE /ADVISED WE ARE RE SETTING /YOUR REST FOR A 2030 DEARTURE /PLZ ACK-THANK YOU  
  
Pilot: GES:50 2 .N24974 ! 5Z 7 Flight UA2781 M35AUA2781/CM CREW DESK / PMDY PHNL 17 160021 PILOT ROGER   
RESET FOR 2030 THNX  
```
  
By this time, some how the media had started to pick up on the adventure and they got some facts wrong or missing.  
[kitv](https://www.kitv.com/story/43689476/mechanical-issue-prompts-ua-flight-to-make-emergency-landing-at-midway-atoll)  
  
[flyertalk](https://www.flyertalk.com/forum/united-airlines-mileageplus/2038144-ua-2781-cargo-only-lax-gum-diverts-midway-atoll-16-april-2021-a.html)  
  
[liveandletsfly](https://liveandletsfly.com/united-787-9-midway-atoll/)  
   
And yet, things were still unfolding, so it was only half the story.  
  
```
Aircraft: GES:50 2 .N24974 ! H1 9 Flight UA2781 E14GUA2781#EIB4; 20 504.4;;6554; 21 CLOSED;CLOSED 22  
NORM;NOT ACTIVE 23 CLOSED;NOT ACTIVE 24 CLOSED;NOT ACTIVE 25 CLOSED;NOT ACTIVE 26 CLOSED 27 ;18;APR;21;00:35:30  
```
  
Typical door closed message, but the timing seemed a bit off. Perhaps the crew closed it and opened it again.  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA R CT AND SECURE EA CONNECTOR TO EA HEATER BELOW FD THROUGH  
ACCESS HATCH. TOMC  
```
  
This one left most of us a little in the dark. The heater and fan were the original issue from what we could gather. Perhaps we missed some details that they exchanged with dispatch via cell or wifi (email).  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA B QUDPCULUA-1MSG FROM OPBLP UA2781/17 PMDY PHNL SENT:   
06:24:49Z GOOD EVENING. . WHEN READY TO GO, . PLEASE LET ME KNOW . IF 750 LBS OF TOOLS . WERE LOADED   
INTO THE . BULK COMPARTMENT. . FINAL WEIGHTS TO . FOLLOW. THANKS. . QUESTIONS – CONTACT LOAD PLANNER  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA D QUDPCULUA.1MSG FROM TOMC UAL2781-17 PMDY PHNL WORKING ON   
YOUR MX RELEASE NOW.  
  
Pilot: GES:50 2 .N24974 ! 5Z 6 Flight UA2781 M41AUA2781/LP LOAD MSG / PMDY PHNL 17 063026 TOOL ARE IN CABIN  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA G QUDPCULUA-1MSG FROM OPBLP UA2781/17 PMDY PHNL SENT:   
06:31:30Z GREAT. ALL 750 LBS . IN CABIN. . . . . . . . QUESTIONS – CONTACT LOAD PLANNER  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA H QUWHQVDUA?1MSG FROM DISP UA2781-17 PMDY PHNL CA PLEASE   
LET ME KNOW WHEN YOU ARE READY TO GO. I NEED TO UPDATE YOUR RELEASE THANKS CHIDD  
  
Dispatch: (this is just part of about a 10 part flight plan release – it gives you a feel for the rest of it.  
AES:A254D8 GES:50 2 .N24974 ! C1 B .DPCULUA 180650 AGM AN .N24974 – – MESSAGE FROM CHIDD – ** PART 02 OF 04 **   
CLEARANCE . . *OFP* (FPL-UAL2781-IN -B789/H-SADE3GHIJ1J2J4J5M1P2RWXYZ/LB1D1 -PMDY0733 -M080F370 DCT MDY DCT   
27N170W/M084F390 DCT 25N165W DCT ECEDO/M083F390 DCT DANNO/M069F310 BOOKE8 -PHNL0227 PHJR -PBN/A1B1C1D1L1O1S2T1   
NAV/RNP2 DAT/1FANS2PDC SUR/260B RSP180 DOF/210418 REG/N24974 EET/PHZH0136 SEL/AFJM CODE/A254D8 OPR/UAL PER/D   
RALT/PHNL RMK/TCAS) TKOF ALTN DIST TIME FUEL 00.00 0 ARWY POSITION MC DIST TIME MOR FL MACH GS/TAS  
ZBO COORDINATES  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! C1 R .DPCULUA 180651 AGM AN .N24974 – FINAL WEIGHTS UA2781/17 PMDY   
PHNL SENT: 06:51:48Z ******************** TOG 374055 TOW CHG – 1130 ZFW 324855 CG 27.4 ********************   
SOB 009 PSGRS 07/000 -007- (48/204) LAP 00 CREW 02/00 KIDS 00 FD JUMPSEAT-0 FA JUMPSEAT-0 ********************   
FLIGHT PLAN RELEASE -2- ********************  
  
Pilot: GES:50 2 .N24974 ! 5Z 6 Flight UA2781 M47AUA2781/LP LOAD MSG / PMDY PHNL 17 070156 250 ONLY WE LEFT 500 HERE. IT WAS MOSTLY COKE ZERO THAT WE LEFT  
```
  
Really nice to hear that they offloaded a good amount of weight in the form of Coke Zero (I’m guessing in a gesture of good will for the Island folk to enjoy for putting them up unannounced).  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA B QUDPCULUA-1INVALID WEIGHTS UA2781/17 PMDY PHNL SENT:   
07:04:49Z INVALID WEIGHTS DUE TO A CHANGE IN FINAL LOAD CONFIGURATION. THE PREVIOUSLY SENT WEIGHTS   
ARE NOW INVALID. NEW WEIGHTS WILL BE SENT AS SOON AS POSSIBLE.  
```
  
Dispatch are re-working the weights as a result of the maintenance guys changing the amount of tools and the Coke Zero offload.  
Its really good to see that rules and regulations are not pushed aside even in times like this.  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! C1 D .DPCULUA 180706 AGM AN .N24974 – FINAL WEIGHTS UA2781/17   
PMDY PHNL SENT: 07:06:24Z ************************ TOG 373555 TOW CHG – 1630 ZFW 324355 CG 27.0   
************************ SOB 009 PSGRS 07/000 -007- (48/204) LAP 00 CREW 02/00 KIDS 00 FD   
JUMPSEAT-0 FA JUMPSEAT-0 ************************ FLIGHT PLAN RELEASE -2- ************************  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA J QUDPCULUA-1MSG FROM OPBLP UA2781/17 PMDY PHNL   
SENT: 07:07:02Z COPY. ONLY 250 LBS . TOOLS IN CABIN. . . FINAL WEIGHTS RESENT.. . HAVE A GREAT   
FLIGHT. . . . QUESTIONS – CONTACT LOAD PLANNER  
```
  
Reminder: (FOB) Fuel was 75.5 when they landed, and is now 56.0 Running the APU for all this time took an expected hit.  
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA S QUDPCULUA-1FINAL WEIGHTS UA2781/17 PMDY PHNL SENT:  
07:12:02Z ******************** TOG 379555 TOW CHG – 1630 ZFW 324355 CG 27.4   
******************** SOB 009 PSGRS 07/000 -007- (48/204) LAP 00 CREW 02/00 KIDS 00 FD   
JUMPSEAT-0 FA JUMPSEAT-0 ******************** FLIGHT PLAN RELEASE ********************  
Dispatach:  
AES:A254D8 GES:50 2 .N24974 ! RA L QUHDQWDUA?1TAKEOFF DATA ** PART 01 OF 01 ** ********************   
T/O MDY 06 7800 FT 787-9 GENX-1B74-75 TEMP 21C ALT 30.12 WIND 350/4 MAG 1KT HW 4KT XW TOCG/TRIM 27.4/3.66   
******************** DRY ******************** *FLAPS 15* ** *ANTI-ICE OFF* ASSMD WT. 380.4  
ASSMD TMP. 64C   
******************** REDUCED EPR -.– N1 *HW* V1 VR V2 88.0 1KT 137 141 145   
******************** TW EPR N1 ATMP V1/VR/V2 0 -.– 88 64C 37/41/45 5 -.– 89 60C 35/40/45 10 -.– 91 55C 33/39/45   
******************** MAX EP  
```
  
About this time, the aircaft sent its first position report via ADSC.  
  
```
Pilot: WE CANT TAKEOFF TILL 0800Z… CAN YOU EXTEND VOID… PLEASE THANX  
```
  
Becasue of birds. They need to take off late so they are all asleep.  
  
```
Dispatch: [freetext] APPROVED AS REQUESTED. REVISED DEPARTURE TIME OF 0800Z VOID TIME 0815  
[freetext] REST OF CLEARANCE REMAINS THE SAME  
```
  
When they depart from these islands with no ATC they have to get clearance from Oakland center which issues the clearance with void times meaning they have to be off in this case by 0815, if not they must get another clearance.   
  
```
Dispatch: AES:A254D8 GES:50 2 .N24974 ! C1 M .DPCULUA 180734 AGM AN .N24974 – UA2781 MDY  
==================MAINTENANCE RELEASE DOCUMENT================   
NOSE/TAIL INBD FLT-DATE-LEG RLS DATE RLS STA-
SEQ-TIME 0974/N24974 2781-16APR21-1 18APR21 MDY 01-0636Z —————————CURRENCIES————————-   
AUTOLAND:AUTOLAND LIMIT LAND 2 6067771 —————–INBOUND PILOT DEFECT REPORTS—————–   
6166173 P 17APR21 MDY DEFECT: DEFERRING BOTH CAPT & F/O SHOULDER HEATERS PER MEL 2145U AS PRECAUTIONARY   
AS THEY RUN IN FLIGHT WHEN RECIRC FANS RUN REF LP 615836. ACTION: 17APR DE  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! C1 A .DPCULUA 180734 AGM AN .N24974 – UA2781 MDY   
==============MAINTENANCE RELEASE DOCUMENT – CONT============= NOSE/TAIL INBD FLT-DATE-LEG RLS DATE   
RLS STA-SEQ-TIME 0974/N24974 2781-16APR21-1 18APR21 MDY 01-0636Z A. THE FOLLOWING MUST OPERATE NORMALLY:   
1. BOTH AIR CONDITIONING PACKS. 2. AT LEAST ONE LEFT CABIN AIR COMPRESSOR. 3. AT LEAST ONE RIGHT CABIN  
AIR COMPRESSOR. 4. REMAINING LOWER RECIRCULATION FAN. NOTE: OPERATE LOWER RECIRC FANS SWITCH NORMALLY  
TO ALLOW REMAINING FAN TO OPERATE.   
******** END MEL 2125L OPS PLACA  
```
  
We got another C-band (satellite dish) ADSC position update from the aircraft.  
They are on the end of the runway.  
  

```
Aircraft: GES:50 2 .N24974 ! BA 1 Flight UA2781 L84AUA2781/OAKODYA.AT1.N24974A1A05E4C3D803B9C181  
B08C681B0ECE6C006A800A327320034A0054FA644C1EE707A6C4E4A0100040EE5A0C48F FANS-1/A CPDLC Message: CPDLC   
Downlink Message: Header: Msg ID: 3 Timestamp: 08:05:57 Message data: POSITION REPORT [positionreport]   
Latitude: 28 09.6′ north Longitude: 176 56.1′ west Time at current position: 08:06 Flight level: 148 Next   
fix: Latitude: 27 00.0′ north Longitude: 170 00.0′ west ETA at next fix: 08:50 Next+1 fix: Latitude:   
25 00.0′ north Longitude: 165 00.0′ west%  
```
  
Pretty typical ACARS position report from the aircraft.  
  
And sure enough, they are on their way to Hawaii.  
  
  
```
Dispatch:  
AES:A254D8 GES:50 2 .N24974 ! RA I QUDPCULUA-1GATE ASSIGN UA2781/17 PMDY PHNL SENT: 08:29:17Z   
*** OUTBOUND FLIGHT IS A QUICK TURN *** GATE G1 OPEN RAMP FREQ OPS FREQ EON 1026Z GROUND PWR   
AVAIL -YES- PLANNED GROUND TIME IS 01:00 NEXT FLT UA2781/18 PHNL KLAX ETD 1130Z  
   
Aircraft:  
GES:50 2 .N24974 ! B6 8 Flight UA2781 L90AUA2781/OAKODYA.ADS.N249741413323438EEC9856E8B9F0D11C  
71C5555498587C8112FD45F32098580453D Waypoint_Change_Event: Lat = 26.9944 Long = -169.992 Alt = 38996 feet.   
Time past the hour = 49m 39s FOM = 1F Next waypoint Lat = 24.9999 Long = -165 Alt = 39000 feet. ETA = 00:33:12  
  
Pilot: GES:50 2 .N24974 ! 5Z 3 Flight UA2781 M79AUA2781/CM CREW DESK / PMDY PHNL 17 085634 PILOT   
HELLO ALL 3 PILOTS WANT TO DV8 AND FLY ON 2781 HNL-LAX WHICH IS THIS PLANE AND IT LEAVES 1 HR AFTER WE  
BLOCK IN…  
   
Pilot: GES:50 2 .N24974 ! 5Z 5 Flight UA2781 M81AUA2781/CM CREW DESK / PMDY PHNL 17 085803 PILOT   
COULD YOU PLZ GET US LISTED ON IT… SINCE ITS A CARGO…  
  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA U 01:00 NEXT FLT UA2781/18 PHNL KLAX ETD 1130Z  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA Y QUDPCULUA-1MSG FROM OPBCM UA2781/17 PMDY PHNL SENT:   
09:43:55Z /HEY CREW, THIS IS THE LATEST INFO WE’VE RECEIVED IN REGARDS TO DEVIATING ON THE CONTINUATION   
OF YOUR FLIGHT. THEY WILL CLEAR CUSTOMS IN HNL AND WILL NOT BE ALLOWED BACK INTO SECURE AREA BC TSA   
WILL BE CLOSED. UNLESS THEY CAN CONVINCE CPB TO ALLOW THEM TO STAY ON THE AIRCRAFT THEY WILL NEED TO   
LAYOVER. THERE IS ALSO NO ONE IN HNL AT THIS HOUR TO PREP ADDITIONAL MEALS. OPBCM DM  
Dispatch: AES:A254D8 GES:50 2 .N24974 ! RA B QUDPCULUA-1MSG FROM OPBCM UA2781/17 PMDY PHNL SENT: 09:45:59Z   
/FOR THE MOMENT I WILL NOT REFLECT YOU TWO DEVIATING IN YOUR PAIRINGS. IF YOU ARE ABLE TO STAY ON THE   
PLANE WHEN YOU GET TO HNL THEN CALL US TO UPDATE PAIRINGS/CXL HOTEL. UNTIL THEN I WILL KEEP YOUR HOTEL   
AND TRANSPORTATION ACTIVE. OPBCM DM  
   
Pilot: GES:50 2 .N24974 ! 5Z 1 Flight UA2781 M94BUA2781 SO MUCH KEEP US POSTED  
```
  
  
ADSC position report from the aircraft, up to the satellite, down to Andrews greound station, uploaded to ADSB Exchange.  
  
And with that they are safely back on track.  
  
I want to thank once again, the guys at ADSB Exhange for ingesting our data and putting up with me on their Discourd server, Andrew for running the 143E station and putting up with my crummy coding ‘skils’ and John in Arizona for prodding me to start this whole ACARS thing in the first place.  
  
--------------------------- EOL --------------------------------------



<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>