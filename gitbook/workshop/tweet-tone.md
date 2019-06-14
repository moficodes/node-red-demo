---
description: Perform Tone analysis of Tweets using the Watson Tone Analyzer service
---

# Tweet Tone

This flow is similar to Sentiment Flow but instead of using Sentiment we will be using Tone Analyzer Service to analyze the tone of the tweet and whether or not it expresses Joy, Fear, Saddness, Anger or Disgust 

![](../.gitbook/assets/image%20%285%29.png)

### How to build this flow

#### Step 1:  Copy Tweet Simple 

Copy the flow from Tweet Simple and paste nodes into this new project 

#### Step 2 : Insert Analyze Tone Service Node 

Insert Analyze Tone Node  from IBM Watson palette and connect to output of function node 

Get Access to Tone Analyzer 

* Log into IBM Cloud and Go to IBM Cloud Catalog 
* Search for Tone Analyzer Service within Catalog

![](../.gitbook/assets/image%20%2821%29.png)



