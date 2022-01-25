# Background of the UAV-Done page.   
   
Navigation: [home](README.md)  

One of the types of aircraft that warranted its very own page on the Node-RED dashboard is UAV or Drones or any of the other names they go under.   

My site uses the ADSBExchange airframe database, drones are classed as different types in there. On top of that people (private and state backed) that build, fly and deploy UAV's don't tend to advertise it. The result of this is I have collected many ICAO hex codes over the past year that may or may not be flagged as UAV in the ADSBEx database.    

Bottom line, I check for both type and ICAO.    

Jan 2022 here is my current list:    
```   
class = ["Q4","Q9","HRON", "Q1","Q25","FRBD", "SOL1", "SOL2","ANKA","DRON"];

icaolist = ["33FD45","33FD5E","33FD69","33FD6A","33FD6B","001453","001071","001084","298CC2","AE5420","43C87E","0200F1","738BE8","AE5C74","AC7B99","738703","425178","AE46B7","AE4BD8","AE4BD9","AE4BDA","AE4BDB","AE540F", "AE5415", "AE54B5","AE541D", "AE54B5", "AE54B6","AE5C72","AE5C73","AE5C74","AE5C76","AE61BB","AE61BC","AE5C16","AE2FD0","AE27A7","AE4BD7","AE4DDE","AE4DDF","44F04E","44F046","44F04C","AC7B99","A4182A","N507HK","N363HK","A61086","4B835F","25E25E"];

```  
If you know of any UAV's that I don't have listed (either by class or hex) please let me know and I can update the code and have a better chance of it showing on the dashboard page.  
    
### Node-RED function block code   
Here is the guts of the function block that finds the UAV needle in the ADSB haystack.    
```  
function twoDig(val) {return (('0'+val).slice(-2));}
var d = new Date();
msg.dts = twoDig(d.getUTCHours())+':'+twoDig(d.getUTCMinutes())+':'+twoDig(d.getUTCSeconds())+'Z ' + twoDig(d.getUTCDate())+'-'+twoDig((d.getUTCMonth()+1))+'-'+d.getUTCFullYear();


droneorno = ["Q4","Q9","HRON", "Q1","Q25","FRBD", "SOL1", "SOL2","ANKA","DRON"];

icaolist = ["33FD45","33FD5E","33FD69","33FD6A","33FD6B","001453","001071","001084","298CC2","AE5420","43C87E","0200F1","738BE8","AE5C74","AC7B99","738703","425178","AE46B7","AE4BD8","AE4BD9","AE4BDA","AE4BDB","AE540F", "AE5415", "AE54B5","AE541D", "AE54B5", "AE54B6","AE5C72","AE5C73","AE5C74","AE5C76","AE61BB","AE61BC","AE5C16","AE2FD0","AE27A7","AE4BD7","AE4DDE","AE4DDF","44F04E","44F046","44F04C","AC7B99","A4182A","N507HK","N363HK","A61086","4B835F","25E25E"];


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