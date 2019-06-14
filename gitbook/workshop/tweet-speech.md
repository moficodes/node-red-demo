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

{% embed url="https://github.com/johnwalicki/Node-RED-Twitter-Workshop/blob/master/flows/Tweet-Speaker.json" %}



