# Background of the UAV-Done page.   
   
Navigation: [home](README.md)  

## Jume 2024.  
While the UAV page from the old site did not make the new site (yet), thebaldgeek is still super interested in these airframes.   
The list here has been updated with the new site launch.    
If you have any thoughts on how to add a UAV table, reach out.   
    
--------
   

One of the types of aircraft that warranted its very own page on the Node-RED dashboard is UAV or Drones or any of the other names they go under.   

My site uses the typical ADSB airframe database, drones are classed as different types in there. On top of that people (private and state backed) that build, fly and deploy UAV's don't tend to advertise it. The result of this is I have collected many ICAO hex codes over the past year that may or may not be flagged as UAV in the ADSB database.    

Bottom line, I check for both type and ICAO.    

June 2024 here is my current list:    
```   
class = ["Q4","Q9","HRON", "Q1","Q25","FRBD", "FFLO", "VFHC", "SOL1", "SOL2","ANKA","DRON", "UAV"];

icaolist = a16c6d,a2f676,a32524,a328db,a33dc3,a4182a,a4724d,a483df,a4bc36,a4bfed,a51a10,a51dc7,a54b56,a54f0d,a552c4,a57343,a5ed09,a5f9f7,a61086,a64217,a645ce,a64985,a654aa,a65861,a66996,a92eee,aa8444,aac551,ac742b,a344e5,acb0cb,acb076,acb175,acb1a0,acb15c,acb1ad,acb234,acb202,ae541a,ae54b7,ae5420,ae5421,ae2c37,ae5411,ae5412,ae5413,ae5417,ae5419,ae625b,ae7811,ae7812,ae7813,ae7814,ae7815,ae7816,af3c53,af4fa8,33fd6b,33fd6a,33fd69,33fd5e,33fd45,87cd20,87cd21,87cd22,71f64a,71f64d,ae51ed,ae5c0d,ae5c13,ae60b7,ac7b99,a5bcc0,ae540e,ae5c76,ae5c71,a169d7,a3c92c,a3c1be,a44360,ae54b6,ae29f8,a410bc,ae27a7,ae2c38,ae2fd0,ae4bd7,a47604,ae61aa,a5b552,add2ef,ae1f0c,ae5422,ae54b5,ae5416,ae5c73,a3e6e3,a67f78,a38569,a5dcb2,A12E51 ,a5d8fb,a5b533,ae17ed,ae5c72,ae5c74,ae5c75,ae625c,ae625d,ae6257,43c889,43c885,43c884,43c883,43c879,43c87a,43c87c,43c87d,43c87e,43c87f,43c810,ad9a7d,43c809,783132,AE6D2F,7CFA7F,7CFA81,7CFA83,7CFA84,7CFA85,7CFA86,7CFA87,7CFA88,7CFA89,7CFA8A,FF6B64,4251CA,42511C,42511D,7CFA7E,7CFA82,7CFA80,AE60C4,AE60BA,AE0FCA,N341HK,506F87,AE541F,43D1F1,N250VU,000003,A2596C,43C888,43C881,43C886,43C87B,43C878,43C887,001453,001071,001084,298CC2,0200F1,738BE8,425178,AE46B7,AE4BDB,AE540F, AE5415,E541D,AE61BB,AE61BC,AE4DDF,44F04E,44F046,44F04C,N507HK,N363HK,4B835F,25E25E,a37c61,ddbdde,001075,00107a,001080,000001,32b32b,32b404,0010a9,000e97,ea810e,00028b,010000,00108f,001085,001077,675645,001265,0055d7,32e239,32e32e,020000,234567,101010,111000,001073,001086,001074,002330,001089,001088,00125f,000290,00028c,0058d8,001260,29cbbf,200000,001261,00107b,001102,ff0a02,249249,47c88d,7a442c,7a442d,7a442f,784090,497024,4b8415

```  
Their are some UAVs that have been tagged with a class and some that are not, so pick a method, tbg suggests ICAO, and stick with it.

If you know of any UAV's that I don't have listed (either by class or hex) please let me know and I can update the code and have a better chance of it showing on the dashboard page.  
    
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