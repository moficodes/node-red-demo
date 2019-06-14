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

{% embed url="https://github.com/johnwalicki/Node-RED-Twitter-Workshop/blob/master/flows/Tweet-Sentiment.json" %}





