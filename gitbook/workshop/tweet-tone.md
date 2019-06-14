---
description: Perform Tone analysis of Tweets using the Watson Tone Analyzer service
---

# Tweet Tone

This flow is similar to Sentiment Flow but instead of using Sentiment we will be using Tone Analyzer Service to analyze the tone of the tweet and whether or not it expresses Joy, Fear, Sadness, Anger or Disgust 

![](../.gitbook/assets/image%20%289%29.png)

### How to build this flow

#### Step 1:  Copy Tweet Simple 

Copy the flow from Tweet Simple and paste nodes into this new project 

#### Step 2 : Insert Analyze Tone Service Node 

Insert Analyze Tone Node  from IBM Watson palette and connect to output of function node 

Get Access to Tone Analyzer 

* Log into IBM Cloud and Go to IBM Cloud Catalog 
* Search for Tone Analyzer Service within Catalog

![](../.gitbook/assets/image%20%284%29.png)

* Create Lite Service 

![](../.gitbook/assets/image%20%2827%29.png)

* Go to created Service and get service credentials for Tone Analyzer 
* Set up node properties with username , password and API key from service credentials 

#### Step 3. Insert Tone Categories , High Score Function and Debug Messages 

1. Insert Change Node and name node **tone\_categories .** Change msg.payload to **msg.response.document\_tone.tone\_categories .** Connect node to Tone Analyzer service

![](../.gitbook/assets/image%20%2811%29.png)

  2.  Insert function node and name node High Score . Connect Node to Tone Analyzer Service and add the code below to filter out emotions from Tone analyzer service and give a score value .  

```text
var emotions = [];
emotions = msg.response.document_tone.tone_categories
                .filter(function(c){
                    if (c.category_id == "emotion_tone")
                    {return c; }
                    })[0].tones;
                    
var myscore =  0;
for (var i=0; i<emotions.length; i++) {
    if(emotions[i].score > myscore) {
        msg.payload = emotions[i].score;
        msg.topic = emotions[i].tone_name;
        myscore = emotions[i].score;
    }
}

return msg;
```

![](../.gitbook/assets/image%20%2830%29.png)

3. Insert Debug Nodes 

* 1 debug node  called Print msg.response with property **msg.response** . This node is connected to tone analyzer 
* 1 debug node called Tone categories with property **msg.payload.**  This node is connected to tone categories 
* 1 debug node called Score with property **msg.topic** . This node is connected to High Score function 

![](../.gitbook/assets/image%20%2820%29.png)

#### Step 4. Insert Switch node and various emotions 

Insert the switch node from the palette and name it Select Emotions 

Set property to msg.topic and connect node to High Score output 

Add 5 properties : 

* ==Joy
* == Sadness 
* == Fear 
* == Anger 
* == Disgust 

Connect Switch node to Change node for each topic and connect Change Node to Template node with property msg.payload 

```text
This tweet expresses {{topic}} - {{tweet.text}}
```

Insert Change Node to Debug node to print output panel 

![](../.gitbook/assets/image%20%2831%29.png)

#### Step 5 : Deploy 

Once this flow is deployed you should be able to see whether a tweet  expresses Joy, Fear , Sadness , Anger or Disgust ! 



### Flow can be imported from : 

{% embed url="https://github.com/johnwalicki/Node-RED-Twitter-Workshop/blob/master/flows/Tweet-Tone.json" %}



