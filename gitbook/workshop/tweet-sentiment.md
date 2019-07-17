---
description: >-
  Search for positive or negative tweets. You could retweet positive tweets or
  SMS tweets to your friends. Sentiment Twitter flow
---

# Tweet Sentiment

This is an addition to Tweet Simple where it takes the output from the function and does sentimental analysis on the tweet and provides a sentimental score . This then prints the score on the debug panel as well as the Positive Tweet or Negative Tweet 

![](../.gitbook/assets/image%20%288%29.png)

### How to Build this Flow 

#### Step 1: Copy The flow from Tweet Simple 

Copy the flow from Tweet Simple and paste nodes into this new project 

#### Step 2. Insert Sentiment Analysis node 

Insert the Sentiment node from the analysis palette and name node. Connect sentiment node to the output of the function node from Tweet Simple 

#### Step 3. Insert Switch Node and Debug Node 

1. Insert switch node and connect it to Sentiment node. Name the property **msg.sentiment.score :** 

* Name the Switch Statement  - Positive / Negative Tweets
* A value of greater or equal to 2 will output positive tweets 
* A value of less than 0 will output negative tweets

![](../.gitbook/assets/image%20%2840%29.png)

   2.  Insert a debug message node and connect it to Sentiment node. Name the property **msg.sentiment.score :**

#### Step 4. Insert Debug nodes for Positive & Negative Tweets 

Insert debug nodes 

* Name one Debug Node : Positive Tweets  
* Name another Debug Node : Negative Tweets 

Make sure both nodes output is msg.payload 

#### Step 5 : Deploy 

You should be able to see the tweet output and sentiment score on the debug pannel 

![](../.gitbook/assets/image%20%287%29.png)

### Flow can be imported from : 

```text
[
   {
      "id":"4a4384ef.679364",
      "type":"tab",
      "label":"Tweet Sentiment",
      "disabled":false,
      "info":""
   },
   {
      "id":"6fc40309.a9816c",
      "type":"debug",
      "z":"4a4384ef.679364",
      "name":"Positive Tweet debug",
      "active":false,
      "tosidebar":true,
      "console":false,
      "tostatus":false,
      "complete":"payload",
      "targetType":"msg",
      "x":920,
      "y":280,
      "wires":[

      ]
   },
   {
      "id":"a0c73e8c.390e9",
      "type":"switch",
      "z":"4a4384ef.679364",
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
            "6fc40309.a9816c"
         ],
         [
            "fdfc97aa.bed388"
         ]
      ]
   },
   {
      "id":"aaf4a123.07ca8",
      "type":"debug",
      "z":"4a4384ef.679364",
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
      "id":"92440481.c4122",
      "type":"twitter in",
      "z":"4a4384ef.679364",
      "twitter":"",
      "tags":"",
      "user":"false",
      "name":"Listen to twitter feed",
      "inputs":1,
      "x":110,
      "y":100,
      "wires":[
         [
            "12c6b877.17c748",
            "fdad13fc.c6eba",
            "da1372e8.e29f4"
         ]
      ]
   },
   {
      "id":"12c6b877.17c748",
      "type":"debug",
      "z":"4a4384ef.679364",
      "name":"msg.tweet details",
      "active":false,
      "console":"false",
      "complete":"tweet",
      "x":490,
      "y":60,
      "wires":[

      ]
   },
   {
      "id":"c42fd386.f0ec5",
      "type":"sentiment",
      "z":"4a4384ef.679364",
      "name":"Sentiment of Tweets",
      "property":"payload",
      "x":350,
      "y":340,
      "wires":[
         [
            "aaf4a123.07ca8",
            "a0c73e8c.390e9"
         ]
      ]
   },
   {
      "id":"fdfc97aa.bed388",
      "type":"debug",
      "z":"4a4384ef.679364",
      "name":"Negative Tweets",
      "active":true,
      "tosidebar":true,
      "console":false,
      "tostatus":false,
      "complete":"payload",
      "targetType":"msg",
      "x":900,
      "y":400,
      "wires":[

      ]
   },
   {
      "id":"fdad13fc.c6eba",
      "type":"function",
      "z":"4a4384ef.679364",
      "name":"Remove URLS and replace #",
      "func":"var tweet = msg.tweet.text;\nvar newtweet = tweet.replace(/#/g, \" Hash tag \");\n\n// regex from https://stackoverflow.com/questions/1500260/detect-urls-in-text-with-javascript\nmsg.payload = newtweet.replace( /(([a-z]+:\\/\\/)?(([a-z0-9\\-]+\\.)+([a-z]{2}|biz|com|co|edu|gov|info|net|org|ly))(:[0-9]{1,5})?(\\/[a-z0-9_\\-\\.~]+)*(\\/([a-z0-9_\\-\\.]*)(\\?[a-z0-9+_\\-\\.%=&amp;]*)?)?(#[a-zA-Z0-9!$&'()*+.=-_~:@/?]*)?)(\\s+|$)/gi, \"see short URL \" );\nreturn msg;",
      "outputs":1,
      "noerr":0,
      "x":520,
      "y":140,
      "wires":[
         [
            "d67a5f93.7583a",
            "c42fd386.f0ec5"
         ]
      ]
   },
   {
      "id":"d67a5f93.7583a",
      "type":"debug",
      "z":"4a4384ef.679364",
      "name":"",
      "active":false,
      "console":"false",
      "complete":"false",
      "x":790,
      "y":140,
      "wires":[

      ]
   },
   {
      "id":"da1372e8.e29f4",
      "type":"debug",
      "z":"4a4384ef.679364",
      "name":"",
      "active":false,
      "console":"false",
      "complete":"tweet.text",
      "x":480,
      "y":100,
      "wires":[

      ]
   },
   {
      "id":"7a4e23f7.3db814",
      "type":"comment",
      "z":"4a4384ef.679364",
      "name":"Pick a #hashtag to follow",
      "info":"",
      "x":120,
      "y":60,
      "wires":[

      ]
   },
   {
      "id":"b9642ad9.8ea61",
      "type":"inject",
      "z":"4a4384ef.679364",
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
            "3c0ac783.efaa58"
         ]
      ]
   },
   {
      "id":"3c0ac783.efaa58",
      "type":"change",
      "z":"4a4384ef.679364",
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
            "fdad13fc.c6eba"
         ]
      ]
   },
   {
      "id":"2075d0f7.dab8c8",
      "type":"inject",
      "z":"4a4384ef.679364",
      "name":"Sadness test",
      "topic":"",
      "payload":"{\"text\":\"This is miserable and sad\"}",
      "payloadType":"json",
      "repeat":"",
      "crontab":"",
      "once":false,
      "onceDelay":"",
      "x":110,
      "y":240,
      "wires":[
         [
            "3c0ac783.efaa58"
         ]
      ]
   },
   {
      "id":"a3e92656.5e6718",
      "type":"inject",
      "z":"4a4384ef.679364",
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
            "3c0ac783.efaa58"
         ]
      ]
   }
]
```





