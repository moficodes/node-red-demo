---
description: Build a Node-RED Dashboard that charts Twitter hashtag sentiment history
---

# Tweet Dashboard

This flow takes the sentiment of tweets and adds them to a dashboard in the form of 

![](../.gitbook/assets/node-red-twitter-tweetdashboard.png)

![](../.gitbook/assets/node-red-twitter-tweetsentiment-dashboard.png)

#### To install Dashboard nodes, your IBM Cloud Instance of Node-RED  needs to be re configured to include dashboard library . 

Here are the steps to configure dashboard nodes in your instance of IBM Cloud : 

**Step 1.** Search for the instance of the Node-RED starter kit you created on IBM Cloud 

![](../.gitbook/assets/screen-shot-2019-07-16-at-6.20.36-pm.png)

**Step 2.** Scroll down to Continuous delivery and click on View toolchain 

![](../.gitbook/assets/screen-shot-2019-07-16-at-6.22.28-pm.png)

**Step 3**.  Click on Git box under Code 

![](../.gitbook/assets/screen-shot-2019-07-16-at-6.23.24-pm.png)



**Step 4** . Once in Git click on package.json 

![](../.gitbook/assets/screen-shot-2019-07-16-at-6.24.53-pm.png)

**Step 5.** Edit package.json dependancies. Add : 

```text
"node-red-dashboard":"2.x" 
```

in the dependency list as so and commit changes 

![](../.gitbook/assets/screen-shot-2019-07-16-at-6.25.34-pm.png)

**Step 6.** Once change is committed go back to App url  and in the manage pallet section search for dashboard nodes 

![](../.gitbook/assets/screen-shot-2019-07-16-at-6.30.29-pm.png)

![](../.gitbook/assets/screen-shot-2019-07-16-at-6.30.35-pm.png)



## Flow can be imported : 

```text
[
    {
        "id": "e44a3241.4c9f8",
        "type": "tab",
        "label": "Tweet Dashboard",
        "disabled": false,
        "info": ""
    },
    {
        "id": "16cbb912.a64787",
        "type": "debug",
        "z": "e44a3241.4c9f8",
        "name": "Positive Tweet debug",
        "active": false,
        "console": "false",
        "complete": "payload",
        "x": 920,
        "y": 280,
        "wires": []
    },
    {
        "id": "50297529.42d9bc",
        "type": "switch",
        "z": "e44a3241.4c9f8",
        "name": "Positive / Negative Tweets",
        "property": "sentiment.score",
        "propertyType": "msg",
        "rules": [
            {
                "t": "gte",
                "v": "2",
                "vt": "num"
            },
            {
                "t": "lt",
                "v": "0",
                "vt": "str"
            }
        ],
        "checkall": "true",
        "outputs": 2,
        "x": 610,
        "y": 340,
        "wires": [
            [
                "16cbb912.a64787"
            ],
            [
                "cd01e2fe.a4184"
            ]
        ]
    },
    {
        "id": "526e45f9.207d84",
        "type": "debug",
        "z": "e44a3241.4c9f8",
        "name": "msg.sentiment.score",
        "active": false,
        "console": "false",
        "complete": "sentiment.score",
        "x": 600,
        "y": 300,
        "wires": []
    },
    {
        "id": "d2d7c66.948b9b8",
        "type": "twitter out",
        "z": "e44a3241.4c9f8",
        "twitter": "",
        "name": "Retweet positive tweets",
        "x": 920,
        "y": 320,
        "wires": []
    },
    {
        "id": "cada3488.bd107",
        "type": "twitter in",
        "z": "e44a3241.4c9f8",
        "twitter": "",
        "tags": "",
        "user": "false",
        "name": "Listen to twitter feed",
        "topic": "tweets",
        "inputs": 1,
        "x": 110,
        "y": 100,
        "wires": [
            [
                "802452c0.f2e1e8",
                "6d278e33.4277b8",
                "dbad27c6.a49e58"
            ]
        ]
    },
    {
        "id": "802452c0.f2e1e8",
        "type": "debug",
        "z": "e44a3241.4c9f8",
        "name": "msg.tweet details",
        "active": false,
        "console": "false",
        "complete": "tweet",
        "x": 490,
        "y": 60,
        "wires": []
    },
    {
        "id": "6b68ea19.79ddac",
        "type": "sentiment",
        "z": "e44a3241.4c9f8",
        "name": "Sentiment of Tweets",
        "x": 350,
        "y": 340,
        "wires": [
            [
                "526e45f9.207d84",
                "50297529.42d9bc",
                "3d44e996.f8a706"
            ]
        ]
    },
    {
        "id": "cd01e2fe.a4184",
        "type": "debug",
        "z": "e44a3241.4c9f8",
        "name": "Negative Tweets",
        "active": false,
        "console": "false",
        "complete": "payload",
        "x": 900,
        "y": 400,
        "wires": []
    },
    {
        "id": "6d278e33.4277b8",
        "type": "function",
        "z": "e44a3241.4c9f8",
        "name": "Remove URLS and replace #",
        "func": "var tweet = msg.tweet.text;\nvar newtweet = tweet.replace(/#/g, \" Hash tag \");\n\n// regex from https://stackoverflow.com/questions/1500260/detect-urls-in-text-with-javascript\nmsg.payload = newtweet.replace( /(([a-z]+:\\/\\/)?(([a-z0-9\\-]+\\.)+([a-z]{2}|biz|com|co|edu|gov|info|net|org|ly))(:[0-9]{1,5})?(\\/[a-z0-9_\\-\\.~]+)*(\\/([a-z0-9_\\-\\.]*)(\\?[a-z0-9+_\\-\\.%=&amp;]*)?)?(#[a-zA-Z0-9!$&'()*+.=-_~:@/?]*)?)(\\s+|$)/gi, \"see short URL \" );\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 520,
        "y": 140,
        "wires": [
            [
                "203bc285.a93b8e",
                "6b68ea19.79ddac"
            ]
        ]
    },
    {
        "id": "203bc285.a93b8e",
        "type": "debug",
        "z": "e44a3241.4c9f8",
        "name": "",
        "active": true,
        "console": "false",
        "complete": "payload",
        "x": 790,
        "y": 140,
        "wires": []
    },
    {
        "id": "dbad27c6.a49e58",
        "type": "debug",
        "z": "e44a3241.4c9f8",
        "name": "",
        "active": false,
        "console": "false",
        "complete": "tweet.text",
        "x": 480,
        "y": 100,
        "wires": []
    },
    {
        "id": "f9e26713.d6ba8",
        "type": "function",
        "z": "e44a3241.4c9f8",
        "name": "Store Tweet data",
        "func": "// tweet object includes a timestamp_ms\nmsg.payload = { \"timestamp\" : msg.tweet.timestamp_ms ,\n                \"tweet\"     : msg.tweet.text,\n                \"sentiment\" : msg.sentiment.score};\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 560,
        "y": 520,
        "wires": [
            [
                "ba632d6c.756a38"
            ]
        ]
    },
    {
        "id": "3d44e996.f8a706",
        "type": "delay",
        "z": "e44a3241.4c9f8",
        "name": "",
        "pauseType": "rate",
        "timeout": "5",
        "timeoutUnits": "seconds",
        "rate": "1",
        "nbRateUnits": "10",
        "rateUnits": "second",
        "randomFirst": "1",
        "randomLast": "5",
        "randomUnits": "seconds",
        "drop": false,
        "x": 340,
        "y": 520,
        "wires": [
            [
                "f2924f4c.58bec",
                "f325f84a.1ca128",
                "f9e26713.d6ba8"
            ]
        ]
    },
    {
        "id": "ba632d6c.756a38",
        "type": "cloudant out",
        "z": "e44a3241.4c9f8",
        "name": "",
        "cloudant": "",
        "database": "tweetdata",
        "service": "IoT-feed-gauge-cloudantNoSQLDB",
        "payonly": true,
        "operation": "insert",
        "x": 760,
        "y": 520,
        "wires": []
    },
    {
        "id": "5e2162cb.3dd674",
        "type": "ui_text",
        "z": "e44a3241.4c9f8",
        "group": "81ae3b38.76278",
        "order": 1,
        "width": 0,
        "height": 0,
        "name": "",
        "label": "",
        "format": "{{msg.payload}}",
        "layout": "row-left",
        "x": 750,
        "y": 560,
        "wires": []
    },
    {
        "id": "6735fe9f.31453",
        "type": "ui_gauge",
        "z": "e44a3241.4c9f8",
        "name": "",
        "group": "626aacb5.62209c",
        "order": 1,
        "width": 0,
        "height": 0,
        "gtype": "gage",
        "title": "Sentiment",
        "label": "units",
        "format": "{{value}}",
        "min": "-10",
        "max": 10,
        "colors": [
            "#00b500",
            "#e6e600",
            "#ca3838"
        ],
        "seg1": "",
        "seg2": "",
        "x": 760,
        "y": 600,
        "wires": []
    },
    {
        "id": "62574da0.ef10b4",
        "type": "ui_chart",
        "z": "e44a3241.4c9f8",
        "name": "",
        "group": "81ae3b38.76278",
        "order": 2,
        "width": 0,
        "height": 0,
        "label": "Tweet Sentiment History",
        "chartType": "line",
        "legend": "false",
        "xformat": "HH:mm:ss",
        "interpolate": "linear",
        "nodata": "",
        "dot": false,
        "ymin": "-10",
        "ymax": "10",
        "removeOlder": 1,
        "removeOlderPoints": "",
        "removeOlderUnit": "3600",
        "cutout": 0,
        "colors": [
            "#1f77b4",
            "#aec7e8",
            "#ff7f0e",
            "#2ca02c",
            "#98df8a",
            "#d62728",
            "#ff9896",
            "#9467bd",
            "#c5b0d5"
        ],
        "useOldStyle": true,
        "x": 750,
        "y": 640,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "f2924f4c.58bec",
        "type": "change",
        "z": "e44a3241.4c9f8",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "tweet.text",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 560,
        "y": 560,
        "wires": [
            [
                "5e2162cb.3dd674"
            ]
        ]
    },
    {
        "id": "f325f84a.1ca128",
        "type": "change",
        "z": "e44a3241.4c9f8",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "sentiment.score",
                "tot": "msg"
            },
            {
                "t": "set",
                "p": "topic",
                "pt": "msg",
                "to": "",
                "tot": "str"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 560,
        "y": 600,
        "wires": [
            [
                "6735fe9f.31453",
                "62574da0.ef10b4"
            ]
        ]
    },
    {
        "id": "b51a1caa.ea8108",
        "type": "inject",
        "z": "e44a3241.4c9f8",
        "name": "Happy test",
        "topic": "",
        "payload": "{\"text\":\"every one is awesome\"}",
        "payloadType": "json",
        "repeat": "",
        "crontab": "",
        "once": false,
        "x": 100,
        "y": 200,
        "wires": [
            [
                "db386e02.e37708"
            ]
        ]
    },
    {
        "id": "db386e02.e37708",
        "type": "change",
        "z": "e44a3241.4c9f8",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "tweet",
                "pt": "msg",
                "to": "payload",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 300,
        "y": 240,
        "wires": [
            [
                "6d278e33.4277b8"
            ]
        ]
    },
    {
        "id": "8a4a4990.c24688",
        "type": "inject",
        "z": "e44a3241.4c9f8",
        "name": "Sadness test",
        "topic": "",
        "payload": "{\"text\":\"This is miserable and sad\"}",
        "payloadType": "json",
        "repeat": "",
        "crontab": "",
        "once": false,
        "x": 110,
        "y": 240,
        "wires": [
            [
                "db386e02.e37708"
            ]
        ]
    },
    {
        "id": "b09eb339.18b138",
        "type": "inject",
        "z": "e44a3241.4c9f8",
        "name": "Angry test",
        "topic": "",
        "payload": "{\"text\":\"I hate this demo\"}",
        "payloadType": "json",
        "repeat": "",
        "crontab": "",
        "once": false,
        "x": 100,
        "y": 280,
        "wires": [
            [
                "db386e02.e37708"
            ]
        ]
    },
    {
        "id": "38056d4f.5ed6c2",
        "type": "twilio out",
        "z": "e44a3241.4c9f8",
        "service": "_ext_",
        "twilio": "e456f1dc.e060b",
        "from": "",
        "number": "",
        "name": "SMS to Phone",
        "x": 900,
        "y": 360,
        "wires": []
    },
    {
        "id": "e6cfad75.ccc9c",
        "type": "comment",
        "z": "e44a3241.4c9f8",
        "name": "Pick a #hashtag to follow",
        "info": "",
        "x": 120,
        "y": 60,
        "wires": []
    },
    {
        "id": "81ae3b38.76278",
        "type": "ui_group",
        "z": "",
        "name": "Tweet Details",
        "tab": "a7fdb82a.1b6f58",
        "order": 1,
        "disp": true,
        "width": "10"
    },
    {
        "id": "626aacb5.62209c",
        "type": "ui_group",
        "z": "",
        "name": "Tweet Scoreboard",
        "tab": "a7fdb82a.1b6f58",
        "order": 2,
        "disp": true,
        "width": "6"
    },
    {
        "id": "e456f1dc.e060b",
        "type": "twilio-api",
        "z": "e44a3241.4c9f8",
        "sid": "",
        "from": "",
        "name": "My Twilio"
    },
    {
        "id": "a7fdb82a.1b6f58",
        "type": "ui_tab",
        "z": "",
        "name": "Tweet Scoreboard",
        "icon": "dashboard",
        "order": 1
    }
]
```



