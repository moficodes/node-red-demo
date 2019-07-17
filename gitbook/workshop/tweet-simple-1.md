---
description: 'Listen for Tweets for a specific word, hashtag or handle'
---

# Tweet Simple

This is a simple flow which listens to a twitter feed and prints the details of the feed on the debug window 

![](../.gitbook/assets/image%20%2826%29.png)

### How to build this flow 

#### Step 1: Drag Twitter Input and Set up Twitter 

Drag the  Twitter input node from the social palette  and double click to set up twitter 

![](../.gitbook/assets/image%20%2824%29.png)

Add your Twitter ID and set up your twitter credentials at : [developer.twitter.com/en/apps](https://developer.twitter.com/en/apps)

![](../.gitbook/assets/image%20%2828%29.png)

Once you have your twitter credentials successfully set up , you can listen for words , @ids  or hashtags 

#### Step 2. Insert Debug and Function Nodes 

1. Insert a Debug node and connect it to Twitter input  and name the output to **msg.tweet**

![](../.gitbook/assets/image%20%2833%29.png)

 2. Insert another Debug node and connect to Twitter Input and name the output **msg.tweet.text**

![](../.gitbook/assets/image%20%2841%29.png)

3 . Insert the function node connected to Twitter Input  with the following code to remove urls from the tweet and replace \# 

```text
// var tweet = msg.tweet.text;
var tweet = msg.payload;
var newtweet = tweet.replace(/#/g, " Hash tag ");

// regex from https://stackoverflow.com/questions/1500260/detect-urls-in-text-with-javascript
msg.payload = newtweet.replace( /(([a-z]+:\/\/)?(([a-z0-9\-]+\.)+([a-z]{2}|biz|com|co|edu|gov|info|net|org|ly))(:[0-9]{1,5})?(\/[a-z0-9_\-\.~]+)*(\/([a-z0-9_\-\.]*)(\?[a-z0-9+_\-\.%=&amp;]*)?)?(#[a-zA-Z0-9!$&'()*+.=-_~:@/?]*)?)(\s+|$)/gi, "see short URL " );
return msg;
```

![](../.gitbook/assets/image%20%2810%29.png)

4. Insert a debug node connected to function Input  and name the output **msg.payload**

#### Step 3.  Deploy Flow 

![](../.gitbook/assets/image%20%2826%29.png)

You should be able to see Tweets on the debug Panel 

### Flow can be imported from : 

```text
  [
   {
      "id":"a7a3d890.3ee768",
      "type":"tab",
      "label":"Tweet Simple",
      "disabled":false,
      "info":""
   },
   {
      "id":"2f047242.9cc9f6",
      "type":"twitter in",
      "z":"a7a3d890.3ee768",
      "twitter":"",
      "tags":"",
      "user":"false",
      "name":"Listen to twitter feed",
      "inputs":1,
      "x":110,
      "y":100,
      "wires":[
         [
            "59368ef7.11b658",
            "6efd9ad1.3e5124",
            "644ea023.1dd318"
         ]
      ]
   },
   {
      "id":"644ea023.1dd318",
      "type":"debug",
      "z":"a7a3d890.3ee768",
      "name":"msg.tweet ",
      "active":true,
      "tosidebar":true,
      "console":false,
      "tostatus":false,
      "complete":"tweet",
      "targetType":"msg",
      "x":470,
      "y":60,
      "wires":[

      ]
   },
   {
      "id":"59368ef7.11b658",
      "type":"function",
      "z":"a7a3d890.3ee768",
      "name":"Remove URLS and replace #",
      "func":"// var tweet = msg.tweet.text;\nvar tweet = msg.payload;\nvar newtweet = tweet.replace(/#/g, \" Hash tag \");\n\n// regex from https://stackoverflow.com/questions/1500260/detect-urls-in-text-with-javascript\nmsg.payload = newtweet.replace( /(([a-z]+:\\/\\/)?(([a-z0-9\\-]+\\.)+([a-z]{2}|biz|com|co|edu|gov|info|net|org|ly))(:[0-9]{1,5})?(\\/[a-z0-9_\\-\\.~]+)*(\\/([a-z0-9_\\-\\.]*)(\\?[a-z0-9+_\\-\\.%=&amp;]*)?)?(#[a-zA-Z0-9!$&'()*+.=-_~:@/?]*)?)(\\s+|$)/gi, \"see short URL \" );\nreturn msg;",
      "outputs":1,
      "noerr":0,
      "x":520,
      "y":140,
      "wires":[
         [
            "4101cbc4.0c83b4"
         ]
      ]
   },
   {
      "id":"4101cbc4.0c83b4",
      "type":"debug",
      "z":"a7a3d890.3ee768",
      "name":"",
      "active":true,
      "tosidebar":true,
      "console":false,
      "tostatus":false,
      "complete":"payload",
      "targetType":"msg",
      "x":790,
      "y":140,
      "wires":[

      ]
   },
   {
      "id":"6efd9ad1.3e5124",
      "type":"debug",
      "z":"a7a3d890.3ee768",
      "name":"",
      "active":true,
      "tosidebar":true,
      "console":false,
      "tostatus":false,
      "complete":"tweet.text",
      "targetType":"msg",
      "x":480,
      "y":100,
      "wires":[

      ]
   },
   {
      "id":"4df098f6.13af",
      "type":"comment",
      "z":"a7a3d890.3ee768",
      "name":"Pick a #hashtag to follow",
      "info":"",
      "x":120,
      "y":60,
      "wires":[

      ]
   }
]
```





