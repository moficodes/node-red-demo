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
        "id": "48e7f9c.bb73308",
        "type": "tab",
        "label": "Tweet Simple",
        "disabled": false,
        "info": ""
    },
    {
        "id": "2baf5713.a4d9b",
        "type": "twitter in",
        "z": "48e7f9c.bb73308",
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
                "45eea513.1f5ddc",
                "b4a49bec.566bc",
                "673ab097.f6d64"
            ]
        ]
    },
    {
        "id": "45eea513.1f5ddc",
        "type": "debug",
        "z": "48e7f9c.bb73308",
        "name": "msg.tweet details",
        "active": true,
        "console": "false",
        "complete": "tweet",
        "x": 490,
        "y": 60,
        "wires": []
    },
    {
        "id": "b4a49bec.566bc",
        "type": "function",
        "z": "48e7f9c.bb73308",
        "name": "Remove URLS and replace #",
        "func": "// var tweet = msg.tweet.text;\nvar tweet = msg.payload;\nvar newtweet = tweet.replace(/#/g, \" Hash tag \");\n\n// regex from https://stackoverflow.com/questions/1500260/detect-urls-in-text-with-javascript\nmsg.payload = newtweet.replace( /(([a-z]+:\\/\\/)?(([a-z0-9\\-]+\\.)+([a-z]{2}|biz|com|co|edu|gov|info|net|org|ly))(:[0-9]{1,5})?(\\/[a-z0-9_\\-\\.~]+)*(\\/([a-z0-9_\\-\\.]*)(\\?[a-z0-9+_\\-\\.%=&amp;]*)?)?(#[a-zA-Z0-9!$&'()*+.=-_~:@/?]*)?)(\\s+|$)/gi, \"see short URL \" );\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 520,
        "y": 140,
        "wires": [
            [
                "34a2442.ccef13c"
            ]
        ]
    },
    {
        "id": "34a2442.ccef13c",
        "type": "debug",
        "z": "48e7f9c.bb73308",
        "name": "",
        "active": true,
        "console": "false",
        "complete": "false",
        "x": 790,
        "y": 140,
        "wires": []
    },
    {
        "id": "673ab097.f6d64",
        "type": "debug",
        "z": "48e7f9c.bb73308",
        "name": "",
        "active": true,
        "console": "false",
        "complete": "tweet.text",
        "x": 480,
        "y": 100,
        "wires": []
    },
    {
        "id": "c5b35fdd.61425",
        "type": "comment",
        "z": "48e7f9c.bb73308",
        "name": "Pick a #hashtag to follow",
        "info": "",
        "x": 120,
        "y": 60,
        "wires": []
    }
]
```





