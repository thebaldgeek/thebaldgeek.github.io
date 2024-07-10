# Background of the UAV-Done page.   
   
Navigation: [home](README.md)  

## Jume 2024.  
While the UAV page from the old site did not make the new site (yet), many #avgeeks are still super interested in these airframes.   
The list here is being updated and maintained by some key avgeeks on X. Big thanks to [Evergreen Intel](https://x.com/vcdgf555).    
If you have any thoughts on what data might be on a UAV table on the website, please reach out.   
    
--------
   
My site uses the typical ADSB airframe database, drones are classed as different `types` in there. On top of that people (private and state backed) that build, fly and deploy UAV's don't tend to advertise it. The result of this is that avgeeks around the world have collected many ICAO hex codes over the past year that may or may not be flagged as UAV in the generic ADSB database.    

Bottom line, tbg finds it of value to check for both type and ICAO.    

July 7th 2024 here is the current list updated by some kind folks on X.:    
```   
type codes = ["Q4","Q9","HRON", "Q1","Q25","FRBD", "FFLO", "VFHC", "SOL1", "SOL2","ANKA","DRON", "UAV"];

icaolist = /?icao=a16c6d,a2f676,a32524,a328db,a33dc3,a4182a,a4724d,a483df,a4bc36,a4bfed,a51a10,a51dc7,a54b56,a54f0d,a552c4,a57343,a5ed09,a5f9f7,a61086,a64217,a645ce,a64985,a654aa,a65861,a66996,a92eee,aa8444,aac551,ac742b,a344e5,acb0cb,acb076,acb175,acb1a0,acb15c,acb1ad,acb234,acb202,ae541a,ae54b7,ae5420,ae5421,ae2c37,ae5411,ae5412,ae5413,ae5417,ae5419,ae625b,ae7811,ae7812,ae7813,ae7814,ae7815,ae7816,af3c53,af4fa8,33fd6b,33fd6a,33fd69,33fd5e,33fd45,87cd20,87cd21,87cd22,71f64a,71f64d,ae51ed,ae5c0d,ae5c13,ae60b7,ac7b99,a5bcc0,ae540e,ae5c76,ae5c71,a169d7,a3c92c,a3c1be,a44360,ae54b6,ae29f8,a410bc,ae27a7,ae2c38,ae2fd0,ae4bd7,a47604,ae61aa,a5b552,add2ef,ae1f0c,ae5422,ae54b5,ae5416,ae5c73,a3e6e3,a67f78,a38569,a5dcb2,a12e51%20,a5d8fb,a5b533,ae17ed,ae5c72,ae5c74,ae5c75,ae625c,ae625d,ae6257,43c889,43c885,43c884,43c883,43c879,43c87a,43c87c,43c87d,43c87e,43c87f,43c810,ad9a7d,43c809,783132,ae6d2f,7cfa7f,7cfa81,7cfa83,7cfa84,7cfa85,7cfa86,7cfa87,7cfa88,7cfa89,7cfa8a,ff6b64,4251ca,42511c,42511d,7cfa7e,7cfa82,7cfa80,ae60c4,ae60ba,ae0fca,506f87,ae541f,43d1f1,000003,a2596c,43c888,43c881,43c886,43c87b,43c878,43c887,001453,001071,001084,298cc2,0200f1,738be8,425178,ae46b7,ae4bdb,ae540f,%20ae5415,ae61bb,ae61bc,ae4ddf,44f04e,44f046,44f04c,4b835f,25e25e,a37c61,ddbdde,001075,00107a,001080,000001,32b32b,32b404,0010a9,000e97,ea810e,00028b,010000,00108f,001085,001077,675645,001265,0055d7,32e239,32e32e,020000,234567,101010,111000,001073,001086,001074,002330,001089,001088,00125f,000290,00028c,0058d8,001260,29cbbf,200000,001261,00107b,001102,ff0a02,249249,47c88d,7a442c,7a442d,7a442f,784090,497024,4b8415,4b83a6,4b8355,4b8349,4b833c,001072,001079,000156,00015c,000457,00057b,000911,000b6d,00106b,001070,001078,001076,00107c,001081,001083,001087,00108d,001092,4d232d,001093,001095,001096,001094,001097,001099,001109,001112,001113,001117,001118,001234,4b8334,4b8335,4b8338,4b8339,4b833a,4b833b,4b8327,4b8328,4b8329,4b832a,4b832b,4b832c,4b832d,4b832e,4b832f,4b8330,4b8331,4b8332,4b8333,4b8336,4b8337,4b833d,4b8354,4b8356,4b8357,4b8358,4b8359,4b835a,4b835b,4b8362,4b835e,4b8360,4b8361,4b834a,00061a,323232,4b834b,4b8370,4b835c,4b8363,4b839d,4b8365,4b8368,4b836d,4b83ef,4b8369,4b836b,4b836e,4b836f,4b8372,4b8374,4b8375,4b8376,4b8378,497cd3,497cdb,4b8414,4b8417,4b83d5,4b839e,497cd2,497cd8,497cd9,497cd0,497cd1,497cda,497cd5,497cd6,497cc8,497ccd,A11111,738be7,738be9,738bea,738beb,AA15AB,3FA757  

```  
    
Copy past the above list and put it on the end of the usual 'globe' URL. Takes about 15 seconds to load all 300+ ICAO's, so just hang in there.

There are some UAVs that have been tagged with a class and some that are not, so pick a method, tbg suggests ICAO, and stick with it.

PLEASE! If you know of any UAV's that are not listed (either by 'type' or ICAO hex) please let tbg know and he can update the list.  
    
### Node-RED function block code   
Here is the guts of the function block that finds the UAV needle in the ADSB haystack.    
```  
function twoDig(val) {return (('0'+val).slice(-2));}
var d = new Date();
msg.dts = twoDig(d.getUTCHours())+':'+twoDig(d.getUTCMinutes())+':'+twoDig(d.getUTCSeconds())+'Z ' + twoDig(d.getUTCDate())+'-'+twoDig((d.getUTCMonth()+1))+'-'+d.getUTCFullYear();


droneorno = ["Q4","Q9","HRON", "Q1","Q25","FRBD", "SOL1", "SOL2","ANKA","DRON"];

icaolist = ["001088","001102","AE0FCA","N341HK","506F87","AE541F","43D1F1","N250VU","000003","A2596C","43C888","43C885","43C884","43C883","43C882","43C881","43C880","43C87F","43C87D","43C87C","43C87A","43C879","43C889","43C886","43C87B","43C878","43C887","33FD45","33FD5E","33FD69","33FD6A","33FD6B","001453","001071","001084","298CC2","AE5420","43C87E","0200F1","738BE8","AE5C74","AC7B99","738703","425178","AE46B7","AE4BD8","AE4BD9","AE4BDA","AE4BDB","AE540F", "AE5415", "AE54B5","AE541D", "AE54B5", "AE54B6","AE5C72","AE5C73","AE5C74","AE5C76","AE61BB","AE61BC","AE2FD0","AE27A7","AE4BD7","AE4DDE","AE4DDF","44F04E","44F046","44F04C","AC7B99","A4182A","N507HK","N363HK","A61086","4B835F","25E25E"];



var megaList = droneorno.concat(icaolist);

for(i = 0; i < megaList.length; i++) {
    if((msg.payload[0].icao.includes(megaList[i])) || (msg.payload[0].type.includes(megaList[i]))) {
        msg.payload = {
            Timestamp:  msg.dts,
            Realtime:   d.getTime(),
            icao:       msg.payload[0].icao,
            Rego:       msg.payload[0].reg,
            Type:       (msg.payload[0].type ? msg.payload[0].type : ""),
            Year:       (msg.payload[0].year? msg.payload[0].year : ""),
            //Interest:   msg.payload[0].interest,
            Desc:       (msg.payload[0].description? msg.payload[0].description : ""),
            Owner:      (msg.payload[0].owner? msg.payload[0].owner : ""),
            Alt:        (msg.raw.alt_baro? msg.raw.alt_baro : ""),
            Speed:      (msg.raw.gs ? msg.raw.gs : ""),
            ADSBEx:     msg.link = "https://globe.adsbexchange.com/?icao="+ msg.payload[0].icao+"&zoom=7&hideSidebar&hidebuttons"
        }
        
        node.send(msg);
    }

    
}   
```
From there things get a little hacky, but the JSON goes into a ui_table node.  
I use the 'screenshot' node to get the centered drone image and use a blank image to show or hide the screenshot of the drone.

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>