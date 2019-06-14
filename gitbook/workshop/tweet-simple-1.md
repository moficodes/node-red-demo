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

{% embed url="https://github.com/johnwalicki/Node-RED-Twitter-Workshop/blob/master/flows/Tweet-Simple.json" %}





