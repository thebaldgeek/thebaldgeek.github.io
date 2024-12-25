# msg by msg break down of interesting ACARS exchanges over a specific flight.   
   
Navigation: [home](README.md)  
   
     
ADSB/C is the where   
ACARS is the why

When you combine the two systems, you end up with a much more accuate telling of the flight.  
On this page thebaldgeek breaks down one (soon two) such flight to show how ACARS explains why ADSB/C folks saw the return, but claimed they did not know why (FlightRadar24, FlightAware (and others) social media teams have done this more than a handful of times - if they can miss ACARS, others might as well).   

QF63 RTB (return to base) flight due to maintance issue. (tbg suspects engine issue)   
Dec 25th 2024.   

thebaldgeek comments in lowercase, ACARS in upper.
   
    
We pick up the flight as they passed the last VHF ACARS receiver over Tasmania and the aircraft switched to satcom.
  
"time": "2024-12-25T00:35:50.033Z",  
"sat": "C-143E",  
MEDIA ADVISORY, VERSION 0:  
LINK VHF ACARS LOST AT 00:35:43 UTC  
AVAILABLE LINKS: DEFAULT SATCOM  
  
tbgmap.airframes.io is the only tar1090 ADSC site around, so it shows tracking beyond Tasmania, ie ADSB range.
The links should take you to the map at the time they are sent.  
  
  
At this timestamp, everything is on track and they get sent arrival overview information from the ground (Note the satcom source is L-Band, that is uplink to the aircraft) and are asked to confirm the ATIS (Air Traffic Information System) sent to the aircrew.  
  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T00:52:28.366Z",  
“(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735087948)",  
VH-OQG JNBATYA.TI2/FAOR ATIS P 0001Z. EXP ZONE IMC ARR RWY03L DEP RWY03L CLEARANCE DELIVERY ON 121. 9  
TRL FL090 WIND 030/9KTS VIS ABV 10KM SCT 600FT BKN 1400FT T16 DP15 QNH 1026HPA TEMPO VIS3000M BCFG  
CONFIRM ATIS  
  
Here is the first sign of the situation unfolding.  
The aircraft via C-Band (from cockpit to ground) request weather reports for New Zealand.  
  
"sat": "C-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T01:15:36.068Z",  
"(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735089336)",  
VH-OQG FLIGHT QF63  
U22AQF0063  
WX REQUEST  
QFA0063/25  
ACTUAL  
FAOR NZFX NZWD  
  
  
Dispatch sends back some data (again, via L-Band. Last time tbg is going to point this out, you get the idea of the flow of satcom by now?).  
  
"icao": "7C4926",  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T01:15:41.335Z",  
“(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735089341)",  
VH-OQG .HDQONQF ~6 01:15 ACTUAL  
METAR TTF FAOR 250100Z 03009KT 9999 BKN005 OVC013 16/15 Q1026 NOSIG=  
AIRPORT DATA MISSING: NZWD  
MISSING WEATHER FOR AIRPORT FOR NZFX  
  
Standard automated position reports are still sent by the system.  
These are of interest and can be plotted.  
Point being, not all L and C band messages are from humans.  
  
"sat": "C-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T01:39:27.113Z",  
"(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735090767)",  
VH-OQG FLIGHT QF63  
J43AQF0063/MELCAYA.ADS.VH-OQG  
BASIC_REPORT:  
LAT = -48.5228 LONG = 140.781 ALT = 34004 FEET. TIME PAST THE HOUR = 39M 18S FOM = 1D  
TRUE TRACK = 207 DEG. GROUND SPEED = 451 KNOTS. VERTICAL RATE = -16 FPM.  
WIND SPEED = 108 KNOTS. TRUE WIND DIRECTION = 281 DEG. TEMPERATURE = -48.5 DEG C.  
NEXT WAYPOINT LAT = -48.7999 LONG = 140.567 ALT = 33996 FEET. ETA = 00:02:38  
  
Crew clearly are working the situation and now request weather data for YPPH (Perth Australia)  
Why so far? They need a good sized airport to land an A388, they need to house a lot of passengers, they need QANTAS maintenance facilities (if possible) and most of all, they need time to burn off fuel and get their landing weight down - more ACARS about this at the end.  
  
"icao": "7C4926",  
"sat": "C-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T03:14:36.892Z",  
"(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735096477)",  
VH-OQG FLIGHT QF63  
U36AQF0063  
WX REQUEST  
QFA0063/25  
ACTUAL FOR YPPH FIMP  
  
Dispatch operators are the unsung heroes of the skies… 10 seconds later they send the METAR report.  
  
  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T03:14:46.534Z",  
"(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735096487)",  
VH-OQG.HDQONQF ~6  
03:14 ACTUAL METAR TTF FAOR 250300Z 07010KT 9000 OVC006 16/14 Q1026 NOSIG=  
METAR YPPH 250300Z 20016KT CAVOK 24/06 Q1016  
RMK RF00.0/000.0=  
SPECI YPPH 250237Z 20015G26KT CAVOK 23/06 Q1016  
RMK RF00.0/000.0=  
METAR FIMP 250300Z 08010KT 9999 FEW018 27/21 Q1016  
  
There are of course voice comm’s going on. A topic for another time.  
Here we see plans change and we now have dispatch send weather for Melbourne, Adelaide and Perth  
  
 "icao": "7C4926",  
 "sat": "L-143E",  
 "type": "A388",  
 "rego": "VH-OQG",  
 "time": "2024-12-25T03:43:56.319Z",  
“(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735098236)",  
VH-OQG  
HDQONQF ~6 03:43   
ATIS YMML P   250329  
APCH: EXP GLS OR ILS APCH  
RWY: WND: 030-160/8. MAX TW 5 KTS WX: CAVOK TMP: 32 QNH: 1012  
-----END OF MESSAGE-----  
ATIS YPAD C   250323  
RWY: 23   WND: 260-320/10. MAX TW 3. MAX XW 15. WX: CAVOK\n\t   TMP: 33  
+ QNH: 1008  
-----END OF MESSAGE-----  
ATIS YPPH X   250310  
APCH: EXP ILS APCH  RWY: 21 AND 24 FOR ARR. RWY 21 FOR DEP.   WND: 200/15 MAX XW 12 KTS, RWY 24  WX: CAVOK  TMP: 24+ QNH: 1015  
-----END OF MESSAGE-----  
  
Dispatch reaching out and checking if the crew need anything.  
Sometimes this sort of check in happens when dispatch operators switch over due to breaks or end of shifts.  
  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T04:37:58.713Z",  
"(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735101479)",  
VH-OQG \tQFFLTDISP~1   
GDAY 63  
DO U REQUIRE ANYTHING FROM  
FLT DISPATCH  
LET ME KNOW IF U DO.  
REGARDS ANDY  
FLT DISPATCH  
  
  
Dispatch letting them know they are going to get some initial landing vectors as they log into the VHF ACARS system over Tasmaina.  
tbg tip ‘freetext’ is an interesting ACARS search term.  
  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T04:40:17.751Z",  
"(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735101618)",  
VH-OQG MELCAYA.AT1.VH-OQG  
FANS-1/A CPDLC MESSAGE:  
CPDLC UPLINK MESSAGE:  
HEADER:   MSG ID: 13 TIMESTAMP: 04:40:11  MESSAGE DATA:  
[FREETEXT]    EXPECT AMENDED ROUTE CLEARANCE ON VHF APPROACHING TASUM  
  
Dispatch letting the crew know the game plan so they can keep the passengers in the loop.  
  
"icao": "7C4926",  
"sat": "L-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T06:14:52.760Z",  
“(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735107293)",   
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
"(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735108042)",  
VH-OQG \tQUSYDKOQF~  
HI PARK BAY: 10  
BAGGAGE CAROUSEL: 15  
A-C OPS 63 JNB 0700+  
FOR THE CSM: ALL PASSENGERS WILL NEED TO FILL IN AN AUSTRALIAN ARRIVAL FORM BEFORE DISEMBARKING.  
WE WILL ADVISE SOON ON ACCOMMODATION DETAILS  
THANKS, QANTAS SYDNEY  
  
This is a ‘fun’ one that tbg does not have an answer to…  
From the flight crew to maintenance that they are going to land a little on the heavy side.  
  
"sat": "C-143E",  
"type": "A388",  
"rego": "VH-OQG",  
"time": "2024-12-25T07:25:40.601Z",  
"(https://tbgmap.airframes.io/?icao=7C4926&showTrace=2024-12-25&timestamp=1735111541)",  
VH-OQG FLIGHT QF63  
U24AQF0063  
TO ENGINEERING  
MAINT QF63 ANTICIPATED LW IS 421000KG. APPROX 30T ABOVE MLW   
  
  
   
  
Check back now and then for updates to this page.     
tbg has one other really cool one he needs to post.     


<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>