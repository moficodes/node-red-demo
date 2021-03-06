---
description: Speak Tweets using the Watson Text to Speech Service from Sentiment Analysis
---

# Tweet Speech

This flow is an addition to Tweet Sentiment \( follow Tweet Sentiment flow \) which 

![](../.gitbook/assets/image%20%2813%29.png)

### How to Build this Flow 

#### Step 1: Copy The flow from Tweet Sentiment

Copy the flow from Tweet Sentiment and paste nodes into this new project 

#### Step 2: Insert delay node 

Insert delay node and set rate for 1 msg per 10 seconds  . This can be changed accodingly. Connect Node to output of switch node to either Positive Tweet or Negative Tweet based on your liking 

#### Step 3 Insert Text to Speech Service 

Insert text to speech node from IBM Watson palette and connect to output of delay node 

Get Access to Text To Speech 

* Log into IBM Cloud and Go to IBM Cloud Catalog 
* Search for Text to Speech Service within Catalog 

![](../.gitbook/assets/image%20%2838%29.png)

* Create Lite Service 

![](../.gitbook/assets/image%20%2839%29.png)

* Go to created Service and get service credentials for Text to Speech node
* Set up node properties with username , password and API key from service credentials 

#### Step 4 : Insert play audio node 

Insert play audio node . Node might need to be installed within the Manage palette in hamburger menu

![](../.gitbook/assets/image%20%2825%29.png)

Go to Manage palette &gt; install and search for play-audio to find node 

Once installed connect node to output of speech to text node 

#### Step 5 : Deploy 

Once this flow is deployed you should be able to hear a tweet that is either positive or negative based on where you connected the speech to text service !  

### Flow can be imported from : 

```text
[
   {
      "id":"68708c76.a7c1f4",
      "type":"tab",
      "label":"Tweet Speech",
      "disabled":false,
      "info":""
   },
   {
      "id":"1e93ff7f.0eb7a9",
      "type":"debug",
      "z":"68708c76.a7c1f4",
      "name":"Positive Tweet debug",
      "active":false,
      "tosidebar":true,
      "console":false,
      "complete":"payload",
      "x":920,
      "y":280,
      "wires":[

      ]
   },
   {
      "id":"ef2349af.8cfa1",
      "type":"switch",
      "z":"68708c76.a7c1f4",
      "name":"Positive / Negative Tweets",
      "property":"sentiment.score",
      "propertyType":"msg",
      "rules":[
         {
            "t":"gte",
            "v":"2",
            "vt":"num"
         },
         {
            "t":"lt",
            "v":"0",
            "vt":"str"
         }
      ],
      "checkall":"true",
      "repair":false,
      "outputs":2,
      "x":610,
      "y":340,
      "wires":[
         [
            "1e93ff7f.0eb7a9",
            "228c4a97.f0d74e"
         ],
         [
            "9dd2969f.a13c",
            "228c4a97.f0d74e"
         ]
      ]
   },
   {
      "id":"1319ac56.d730c4",
      "type":"debug",
      "z":"68708c76.a7c1f4",
      "name":"msg.sentiment.score",
      "active":true,
      "tosidebar":true,
      "console":false,
      "tostatus":false,
      "complete":"sentiment.score",
      "targetType":"msg",
      "x":600,
      "y":300,
      "wires":[

      ]
   },
   {
      "id":"c8eb62e6.80fc68",
      "type":"twitter in",
      "z":"68708c76.a7c1f4",
      "twitter":"",
      "tags":"",
      "user":"false",
      "name":"Listen to twitter feed",
      "inputs":1,
      "x":110,
      "y":100,
      "wires":[
         [
            "22950596.3fd8ea",
            "f5b2c419.009468",
            "60fd6055.7ce428"
         ]
      ]
   },
   {
      "id":"22950596.3fd8ea",
      "type":"debug",
      "z":"68708c76.a7c1f4",
      "name":"msg.tweet details",
      "active":true,
      "console":"false",
      "complete":"tweet",
      "x":490,
      "y":60,
      "wires":[

      ]
   },
   {
      "id":"ee436314.1ff58",
      "type":"sentiment",
      "z":"68708c76.a7c1f4",
      "name":"Sentiment of Tweets",
      "property":"payload",
      "x":350,
      "y":340,
      "wires":[
         [
            "1319ac56.d730c4",
            "ef2349af.8cfa1"
         ]
      ]
   },
   {
      "id":"9dd2969f.a13c",
      "type":"debug",
      "z":"68708c76.a7c1f4",
      "name":"Negative Tweets",
      "active":false,
      "console":"false",
      "complete":"payload",
      "x":900,
      "y":400,
      "wires":[

      ]
   },
   {
      "id":"60fd6055.7ce428",
      "type":"function",
      "z":"68708c76.a7c1f4",
      "name":"Remove URLS and replace #",
      "func":"var tweet = msg.tweet.text;\nvar newtweet = tweet.replace(/#/g, \" Hash tag \");\n\n// regex from https://stackoverflow.com/questions/1500260/detect-urls-in-text-with-javascript\nmsg.payload = newtweet.replace( /(([a-z]+:\\/\\/)?(([a-z0-9\\-]+\\.)+([a-z]{2}|biz|com|co|edu|gov|info|net|org|ly))(:[0-9]{1,5})?(\\/[a-z0-9_\\-\\.~]+)*(\\/([a-z0-9_\\-\\.]*)(\\?[a-z0-9+_\\-\\.%=&amp;]*)?)?(#[a-zA-Z0-9!$&'()*+.=-_~:@/?]*)?)(\\s+|$)/gi, \"see short URL \" );\nreturn msg;",
      "outputs":1,
      "noerr":0,
      "x":520,
      "y":140,
      "wires":[
         [
            "309ce339.21c75c",
            "ee436314.1ff58"
         ]
      ]
   },
   {
      "id":"309ce339.21c75c",
      "type":"debug",
      "z":"68708c76.a7c1f4",
      "name":"",
      "active":true,
      "console":"false",
      "complete":"false",
      "x":790,
      "y":140,
      "wires":[

      ]
   },
   {
      "id":"f5b2c419.009468",
      "type":"debug",
      "z":"68708c76.a7c1f4",
      "name":"",
      "active":true,
      "console":"false",
      "complete":"tweet.text",
      "x":480,
      "y":100,
      "wires":[

      ]
   },
   {
      "id":"635daaec.36289c",
      "type":"comment",
      "z":"68708c76.a7c1f4",
      "name":"node-red-node-watson dependency",
      "info":"This flow requires the\n  node-red-node-watson@0.5.10 or higher\nfor the following Watson nodes:\n  Text to Speech\n  Speech to Text\n  Tone Analyzer\n  Visual Recognition\n\nYou can either \n  $ sudo npm -g install node-red-node-watson\n  and restart the Node-RED service\nor install it from Node-RED Manage Palette.",
      "x":510,
      "y":560,
      "wires":[

      ]
   },
   {
      "id":"4a507bd1.a5635c",
      "type":"comment",
      "z":"68708c76.a7c1f4",
      "name":"node-red-contrib-play-audio dependency",
      "info":"This flow requires the\n  node-red-contrib-play-audio\nfor the Browser play audio node.\nYou can either \n  $ sudo npm -g install node-red-contrib-play-audio\n  and restart the Node-RED service\nor install it from Node-RED Manage Palette.",
      "x":1060,
      "y":580,
      "wires":[

      ]
   },
   {
      "id":"228c4a97.f0d74e",
      "type":"delay",
      "z":"68708c76.a7c1f4",
      "name":"",
      "pauseType":"rate",
      "timeout":"5",
      "timeoutUnits":"seconds",
      "rate":"1",
      "nbRateUnits":"10",
      "rateUnits":"second",
      "randomFirst":"1",
      "randomLast":"5",
      "randomUnits":"seconds",
      "drop":false,
      "x":340,
      "y":520,
      "wires":[
         [
            "dec87853.5d85b8"
         ]
      ]
   },
   {
      "id":"1045d97a.d2cc2f",
      "type":"comment",
      "z":"68708c76.a7c1f4",
      "name":"Paste API keys for Watson Text to Speech",
      "info":"1. Log into IBM Cloud\n2. Create an instance of the \nWatson Text to Speech service.\n3. Visit the Service Credentials tab\n4. Click on View Credentials\n5. Copy/Paste the password and username into\nthis Node-RED node.\n\nOr\n1. Open this Cloud Foundry Node-RED Starter App\n2. Create a new Connection\n3. Bind the Watson Text to Speech service\n4. Restage your Cloud Foundry application",
      "x":600,
      "y":480,
      "wires":[

      ]
   },
   {
      "id":"de143b55.310c8",
      "type":"inject",
      "z":"68708c76.a7c1f4",
      "name":"Happy test",
      "topic":"",
      "payload":"{\"text\":\"every one is awesome\"}",
      "payloadType":"json",
      "repeat":"",
      "crontab":"",
      "once":false,
      "onceDelay":"",
      "x":100,
      "y":200,
      "wires":[
         [
            "834206f6.de9f18"
         ]
      ]
   },
   {
      "id":"834206f6.de9f18",
      "type":"change",
      "z":"68708c76.a7c1f4",
      "name":"",
      "rules":[
         {
            "t":"set",
            "p":"tweet",
            "pt":"msg",
            "to":"payload",
            "tot":"msg"
         }
      ],
      "action":"",
      "property":"",
      "from":"",
      "to":"",
      "reg":false,
      "x":300,
      "y":240,
      "wires":[
         [
            "60fd6055.7ce428"
         ]
      ]
   },
   {
      "id":"f7a31812.9c6008",
      "type":"inject",
      "z":"68708c76.a7c1f4",
      "name":"Sadness test",
      "topic":"",
      "payload":"{\"text\":\"Rainy days make me sad\"}",
      "payloadType":"json",
      "repeat":"",
      "crontab":"",
      "once":false,
      "onceDelay":"",
      "x":110,
      "y":240,
      "wires":[
         [
            "834206f6.de9f18"
         ]
      ]
   },
   {
      "id":"f9c86374.9608c8",
      "type":"inject",
      "z":"68708c76.a7c1f4",
      "name":"Angry test",
      "topic":"",
      "payload":"{\"text\":\"I hate this demo\"}",
      "payloadType":"json",
      "repeat":"",
      "crontab":"",
      "once":false,
      "x":100,
      "y":280,
      "wires":[
         [
            "834206f6.de9f18"
         ]
      ]
   },
   {
      "id":"cf9ddff3.c8a03",
      "type":"comment",
      "z":"68708c76.a7c1f4",
      "name":"Pick a #hashtag to follow",
      "info":"",
      "x":120,
      "y":60,
      "wires":[

      ]
   },
   {
      "id":"dec87853.5d85b8",
      "type":"watson-text-to-speech",
      "z":"68708c76.a7c1f4",
      "name":"text to speech",
      "lang":"en-US",
      "langhidden":"en-US",
      "langcustom":"NoCustomisationSetting",
      "langcustomhidden":"",
      "voice":"en-US_AllisonV2Voice",
      "voicehidden":"en-US_AllisonV2Voice",
      "format":"audio/wav",
      "password":"Go3dEL-Escher-B@ch-climB-0ak5!",
      "apikey":"YptiEGxP7PZK71dQVZq96jBmZZ7Y9KxJcDwYO9Kt5WWp",
      "payload-response":false,
      "default-endpoint":true,
      "service-endpoint":"https://stream.watsonplatform.net/text-to-speech/api",
      "x":560,
      "y":520,
      "wires":[
         [
            "72f524c5.005904"
         ]
      ]
   },
   {
      "id":"72f524c5.005904",
      "type":"play audio",
      "z":"68708c76.a7c1f4",
      "name":"",
      "voice":"0",
      "x":1010,
      "y":520,
      "wires":[

      ]
   }
]
```



