# A flow to automatically get TLE data from celestrak.com and use it with the satellites node   
   
Navigation: [home](README.md)
   
## Jume 2024. Ignore this page    
Do not use. Celestrak changed their endpoints around mid 2023 and broke 100's of TLE updators. tbg has not updated this flow to reflect that breaking change.        

There are two parts to consider here.   
You should not hit the URL every time you want to track the satellite or move the rotator. To pull this off, we get the TLE once every 24 hours (plenty fast enough for most satellite orbits) and store it in a flow.context list, then every time we want to move the rotator or get the satellite position data we read the TLE out of the flow.context list.   
This example uses 25E Alphasat as its example. Just change the satellite number for your object of tracking choice.
    
With all that said, here is the flow:   
   
    [{"id":"ff478ce1.f0b78","type":"inject","z":"dac61f27.3a12b8","name":"24 hours","props":[{"p":"payload"}],"repeat":"86400","crontab":"","once":true,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":1420,"y":1140,"wires":[["7f94c7f5.78a3d8"]]},{"id":"7aaf15aa.0224dc","type":"debug","z":"dac61f27.3a12b8","name":"","active":false,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","targetType":"full","statusVal":"","statusType":"auto","x":2210,"y":1240,"wires":[]},{"id":"7f94c7f5.78a3d8","type":"http request","z":"dac61f27.3a12b8","name":"get 25E TLE","method":"GET","ret":"txt","paytoqs":"ignore","url":"https://celestrak.com/satcat/tle.php?CATNR=39215","tls":"","persist":false,"proxy":"","authType":"","x":1600,"y":1140,"wires":[["76626a71.02b424"]]},{"id":"30bd0a6b.dcf856","type":"tle","z":"dac61f27.3a12b8","satid":"","tle1":"","tle2":"","coordsys":"latlongdeg","name":"25E Alphasat","x":2020,"y":1240,"wires":[["7aaf15aa.0224dc"]]},{"id":"7ee3cc64.1568f4","type":"debug","z":"dac61f27.3a12b8","name":"","active":false,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","targetType":"full","statusVal":"","statusType":"auto","x":1930,"y":1180,"wires":[]},{"id":"76626a71.02b424","type":"function","z":"dac61f27.3a12b8","name":"set","func":"// From the returned string, split on new line and build\n//an array of sat, tle1 and tle2\n//then store it in the 'flow' memory so we can use it every 15min to drive the dish.\n\nlist = msg.payload.split('\\n');\nflow.set(\"25list\", list);\n\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","libs":[],"x":1800,"y":1140,"wires":[["d7e3839d.1f54f"]]},{"id":"ca011185.37668","type":"function","z":"dac61f27.3a12b8","name":"get 25list","func":"// Get the TLE from the flow memory and feed it into the array and feed that into the sat node\n// (All this so we don't pound the celestrak website every 15 minutes needlessly)\n\nlist = flow.get(\"25list\");\nmsg.payload = list;\n\nreturn msg;","outputs":1,"noerr":0,"initialize":"","finalize":"","libs":[],"x":1580,"y":1240,"wires":[["4735b9e9.3dbc68","64941ac2.789ef4"]]},{"id":"d39902e0.20b55","type":"inject","z":"dac61f27.3a12b8","name":"15 minutes","props":[{"p":"payload"}],"repeat":"900","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":1430,"y":1240,"wires":[["ca011185.37668"]]},{"id":"d7e3839d.1f54f","type":"debug","z":"dac61f27.3a12b8","name":"","active":false,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","targetType":"full","statusVal":"","statusType":"auto","x":1980,"y":1140,"wires":[]},{"id":"64941ac2.789ef4","type":"debug","z":"dac61f27.3a12b8","name":"","active":false,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","targetType":"full","statusVal":"","statusType":"auto","x":1710,"y":1180,"wires":[]},{"id":"4735b9e9.3dbc68","type":"change","z":"dac61f27.3a12b8","name":"tweak the payload","rules":[{"t":"set","p":"satid","pt":"msg","to":"payload[0]","tot":"msg"},{"t":"set","p":"tle1","pt":"msg","to":"payload[1]","tot":"msg"},{"t":"set","p":"tle2","pt":"msg","to":"payload[2]","tot":"msg"},{"t":"set","p":"timestamp","pt":"msg","to":"","tot":"date"},{"t":"delete","p":"payload","pt":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":1770,"y":1240,"wires":[["30bd0a6b.dcf856","7ee3cc64.1568f4"]]}]

This next flow includes the above auto-TLE and adds some first steps to dish tracking.   
Before installing this next flow, there are some extra nodes you need to add to your Node-RED. Just click on the menu (top right) and then manage pallet, from there, click the install tab and be sure to type out the whole node, its too easy to install the wrong dashboard if you just type 'dashboard' for example, but if you use the full name you will get the right ones.   
     
[node-red-contrib-satellites](https://flows.nodered.org/node/node-red-contrib-satellites)    
[node-red-dashboard](https://flows.nodered.org/node/node-red-dashboard)    
[node-red-node-ui-table](https://flows.nodered.org/node/node-red-node-ui-table)
    
Install them one at a time, wait till you get the green slider at the top saying its been installed before you do the next one.   
Once all those are installed, then copy paste this flow.   
   

```   

[
    {
        "id": "03f577b3e8eaa50a",
        "type": "tab",
        "label": "C-Band Dish",
        "disabled": false,
        "info": "",
        "env": []
    },
    {
        "id": "ff478ce1.f0b78",
        "type": "inject",
        "z": "03f577b3e8eaa50a",
        "name": "24 hours",
        "props": [
            {
                "p": "payload"
            }
        ],
        "repeat": "86400",
        "crontab": "",
        "once": true,
        "onceDelay": "5",
        "topic": "",
        "payload": "",
        "payloadType": "date",
        "x": 180,
        "y": 100,
        "wires": [
            [
                "7f94c7f5.78a3d8"
            ]
        ]
    },
    {
        "id": "7f94c7f5.78a3d8",
        "type": "http request",
        "z": "03f577b3e8eaa50a",
        "name": "get 98W TLE",
        "method": "GET",
        "ret": "txt",
        "paytoqs": "ignore",
        "url": "https://celestrak.com/satcat/tle.php?CATNR=33278",
        "tls": "",
        "persist": false,
        "proxy": "",
        "authType": "",
        "senderr": false,
        "x": 350,
        "y": 100,
        "wires": [
            [
                "76626a71.02b424",
                "61e0e359.fcf854"
            ]
        ]
    },
    {
        "id": "76626a71.02b424",
        "type": "function",
        "z": "03f577b3e8eaa50a",
        "name": "save TLE",
        "func": "// From the returned string, split on new line and build\n//an array of sat, tle1 and tle2\n//then store it in the 'flow' memory so we can use it every 15min to drive the dish.\n\nlist = msg.payload.split('\\n');\nflow.set(\"98tle\", list);\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 560,
        "y": 100,
        "wires": [
            []
        ]
    },
    {
        "id": "b707790a.f6a868",
        "type": "inject",
        "z": "03f577b3e8eaa50a",
        "name": "15 mins",
        "props": [
            {
                "p": "payload"
            }
        ],
        "repeat": "900",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "",
        "payloadType": "date",
        "x": 160,
        "y": 420,
        "wires": [
            [
                "ca011185.37668"
            ]
        ]
    },
    {
        "id": "ca011185.37668",
        "type": "function",
        "z": "03f577b3e8eaa50a",
        "name": "get 98 TLE",
        "func": "// Get the TLE from the flow memory and feed it into the array and feed that into the sat node\n// (All this so we don't pound the celestrak website every 15 minutes needlessly)\n\nlist = flow.get(\"98tle\");\nmsg.payload = list;\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 370,
        "y": 420,
        "wires": [
            [
                "4735b9e9.3dbc68"
            ]
        ]
    },
    {
        "id": "4735b9e9.3dbc68",
        "type": "change",
        "z": "03f577b3e8eaa50a",
        "name": "tweak the payload",
        "rules": [
            {
                "t": "set",
                "p": "satid",
                "pt": "msg",
                "to": "payload[0]",
                "tot": "msg"
            },
            {
                "t": "set",
                "p": "tle1",
                "pt": "msg",
                "to": "payload[1]",
                "tot": "msg"
            },
            {
                "t": "set",
                "p": "tle2",
                "pt": "msg",
                "to": "payload[2]",
                "tot": "msg"
            },
            {
                "t": "set",
                "p": "timestamp",
                "pt": "msg",
                "to": "",
                "tot": "date"
            },
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 495,
        "y": 420,
        "wires": [
            [
                "3c95bba62432c31a"
            ]
        ],
        "l": false
    },
    {
        "id": "2d5b96de.30473a",
        "type": "ui_chart",
        "z": "03f577b3e8eaa50a",
        "name": "Inmarsat 98W orbit",
        "group": "320e2d891bc6a744",
        "order": 8,
        "width": 15,
        "height": 10,
        "label": "",
        "chartType": "line",
        "legend": "false",
        "xformat": "HH:mm",
        "interpolate": "linear",
        "nodata": "",
        "dot": false,
        "ymin": "-5",
        "ymax": "5",
        "removeOlder": "2",
        "removeOlderPoints": "",
        "removeOlderUnit": "86400",
        "cutout": 0,
        "useOneColor": false,
        "useUTC": false,
        "colors": [
            "#1f77b4",
            "#ff8000",
            "#c0c0c0",
            "#2ca02c",
            "#98df8a",
            "#d62728",
            "#ff9896",
            "#9467bd",
            "#c5b0d5"
        ],
        "outputs": 1,
        "useDifferentColor": false,
        "className": "",
        "x": 1070,
        "y": 420,
        "wires": [
            []
        ]
    },
    {
        "id": "3c95bba62432c31a",
        "type": "tle",
        "z": "03f577b3e8eaa50a",
        "satid": "",
        "tle1": "",
        "tle2": "",
        "coordsys": "",
        "name": "",
        "x": 660,
        "y": 420,
        "wires": [
            [
                "f8d47e4fe026f67c",
                "e198a4e9973e9c73",
                "e795df546d3e0ea9",
                "71cc19f0.d30638"
            ]
        ]
    },
    {
        "id": "f8d47e4fe026f67c",
        "type": "change",
        "z": "03f577b3e8eaa50a",
        "name": "move lat to payload",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "payload.position.lat",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 840,
        "y": 420,
        "wires": [
            [
                "2d5b96de.30473a"
            ]
        ]
    },
    {
        "id": "63d149f1727638ce",
        "type": "comment",
        "z": "03f577b3e8eaa50a",
        "name": "Every 24 hours get the latest TLE",
        "info": "",
        "x": 270,
        "y": 40,
        "wires": []
    },
    {
        "id": "720991eb681e8db4",
        "type": "comment",
        "z": "03f577b3e8eaa50a",
        "name": "Every 15 minutes update the graph (and send the new resistance value to the dish controller)",
        "info": "",
        "x": 400,
        "y": 360,
        "wires": []
    },
    {
        "id": "7126743df51ed653",
        "type": "debug",
        "z": "03f577b3e8eaa50a",
        "name": "",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 1310,
        "y": 600,
        "wires": []
    },
    {
        "id": "e198a4e9973e9c73",
        "type": "debug",
        "z": "03f577b3e8eaa50a",
        "name": "",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "true",
        "targetType": "full",
        "statusVal": "",
        "statusType": "auto",
        "x": 810,
        "y": 380,
        "wires": []
    },
    {
        "id": "61e0e359.fcf854",
        "type": "split",
        "z": "03f577b3e8eaa50a",
        "name": "split on space",
        "splt": " ",
        "spltType": "str",
        "arraySplt": 1,
        "arraySpltType": "len",
        "stream": false,
        "addname": "",
        "x": 580,
        "y": 160,
        "wires": [
            [
                "dd61ce19.4dc02"
            ]
        ]
    },
    {
        "id": "dd61ce19.4dc02",
        "type": "join",
        "z": "03f577b3e8eaa50a",
        "name": "",
        "mode": "custom",
        "build": "array",
        "property": "payload",
        "propertyType": "msg",
        "key": "topic",
        "joiner": "\\n",
        "joinerType": "str",
        "accumulate": false,
        "timeout": "",
        "count": "",
        "reduceRight": false,
        "reduceExp": "",
        "reduceInit": "",
        "reduceInitType": "",
        "reduceFixup": "",
        "x": 750,
        "y": 160,
        "wires": [
            [
                "1c7e2520.91eb93"
            ]
        ]
    },
    {
        "id": "1c7e2520.91eb93",
        "type": "function",
        "z": "03f577b3e8eaa50a",
        "name": "get date",
        "func": "msg.year = msg.payload[17].substring(0,2);\nmsg.day = msg.payload[17].substring(2,5);\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "x": 900,
        "y": 160,
        "wires": [
            [
                "886cfdf49b1d3ade",
                "7d0643f9c7ae82a6",
                "4e3a719ca8d24a35"
            ]
        ]
    },
    {
        "id": "886cfdf49b1d3ade",
        "type": "debug",
        "z": "03f577b3e8eaa50a",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "true",
        "targetType": "full",
        "statusVal": "",
        "statusType": "auto",
        "x": 1090,
        "y": 160,
        "wires": []
    },
    {
        "id": "7d0643f9c7ae82a6",
        "type": "ui_text",
        "z": "03f577b3e8eaa50a",
        "group": "320e2d891bc6a744",
        "order": 3,
        "width": 3,
        "height": 1,
        "name": "",
        "label": "TLE Year: ",
        "format": "{{msg.year}}",
        "layout": "row-left",
        "className": "",
        "x": 1100,
        "y": 120,
        "wires": []
    },
    {
        "id": "4e3a719ca8d24a35",
        "type": "ui_text",
        "z": "03f577b3e8eaa50a",
        "group": "320e2d891bc6a744",
        "order": 1,
        "width": 3,
        "height": 1,
        "name": "",
        "label": "TLE Day: ",
        "format": "{{msg.day}}",
        "layout": "row-left",
        "className": "",
        "x": 1100,
        "y": 80,
        "wires": []
    },
    {
        "id": "e795df546d3e0ea9",
        "type": "function",
        "z": "03f577b3e8eaa50a",
        "name": "clean up lat/lon",
        "func": "msg.lat = msg.payload.position.lat.toFixed(2);\nmsg.lon = msg.payload.position.lon.toFixed(2);\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 840,
        "y": 500,
        "wires": [
            [
                "79bcf3e263428bae",
                "6c289c645a400d4b"
            ]
        ]
    },
    {
        "id": "79bcf3e263428bae",
        "type": "ui_text",
        "z": "03f577b3e8eaa50a",
        "group": "320e2d891bc6a744",
        "order": 5,
        "width": 4,
        "height": 1,
        "name": "",
        "label": "Current Lat: ",
        "format": "{{msg.lat}}",
        "layout": "row-left",
        "className": "",
        "x": 1050,
        "y": 480,
        "wires": []
    },
    {
        "id": "6c289c645a400d4b",
        "type": "ui_text",
        "z": "03f577b3e8eaa50a",
        "group": "320e2d891bc6a744",
        "order": 6,
        "width": 4,
        "height": 1,
        "name": "",
        "label": "Current Lon: ",
        "format": "{{msg.lon}}",
        "layout": "row-left",
        "className": "",
        "x": 1050,
        "y": 520,
        "wires": []
    },
    {
        "id": "71cc19f0.d30638",
        "type": "range",
        "z": "03f577b3e8eaa50a",
        "minin": "3.5",
        "maxin": "-3.5",
        "minout": "7500",
        "maxout": "2300",
        "action": "scale",
        "round": true,
        "property": "payload.position.lat",
        "name": "map lat to dish resitor",
        "x": 860,
        "y": 600,
        "wires": [
            [
                "debe50c6.14231"
            ]
        ]
    },
    {
        "id": "debe50c6.14231",
        "type": "change",
        "z": "03f577b3e8eaa50a",
        "name": "lat to payload",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "payload.position.lat",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1070,
        "y": 600,
        "wires": [
            [
                "7126743df51ed653",
                "f01b0bc554fc5ff4"
            ]
        ]
    },
    {
        "id": "f01b0bc554fc5ff4",
        "type": "ui_text",
        "z": "03f577b3e8eaa50a",
        "group": "320e2d891bc6a744",
        "order": 6,
        "width": "6",
        "height": 1,
        "name": "",
        "label": "Dish resistance cmd: ",
        "format": "{{msg.payload}}",
        "layout": "row-left",
        "className": "",
        "x": 1340,
        "y": 560,
        "wires": []
    },
    {
        "id": "5a4a1a318e1c5b44",
        "type": "comment",
        "z": "03f577b3e8eaa50a",
        "name": "Connect this to dish Pi to drive arm to this value.",
        "info": "",
        "x": 1420,
        "y": 640,
        "wires": []
    },
    {
        "id": "cf9b97399030d247",
        "type": "comment",
        "z": "03f577b3e8eaa50a",
        "name": "Change resistance values here to match your dish.",
        "info": "",
        "x": 850,
        "y": 640,
        "wires": []
    },
    {
        "id": "aa328414acbe7ff3",
        "type": "ui_spacer",
        "z": "03f577b3e8eaa50a",
        "name": "spacer",
        "group": "320e2d891bc6a744",
        "order": 2,
        "width": "1",
        "height": "1"
    },
    {
        "id": "4e626413412a6b29",
        "type": "ui_spacer",
        "z": "03f577b3e8eaa50a",
        "name": "spacer",
        "group": "320e2d891bc6a744",
        "order": 4,
        "width": "8",
        "height": "1"
    },
    {
        "id": "a579bc59de10e8d4",
        "type": "ui_spacer",
        "z": "03f577b3e8eaa50a",
        "name": "spacer",
        "group": "320e2d891bc6a744",
        "order": 7,
        "width": "7",
        "height": "1"
    },
    {
        "id": "320e2d891bc6a744",
        "type": "ui_group",
        "name": "98W -  4F1 - Orbit Data",
        "tab": "c2728698.dcf648",
        "order": 2,
        "disp": true,
        "width": "15",
        "collapse": false,
        "className": ""
    },
    {
        "id": "c2728698.dcf648",
        "type": "ui_tab",
        "name": "C-Band ACARS",
        "icon": "dashboard",
        "order": 1,
        "disabled": false,
        "hidden": false
    }
]   
  
```
More to come.

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-HGJWTNL65R"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-HGJWTNL65R');
</script>