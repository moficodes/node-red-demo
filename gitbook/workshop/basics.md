---
description: >-
  Node-RED is an awesome tool that makes prototyping a lot faster and easier!
  Node-RED is very easy to get started with and is a great tool for beginners
  who want to write and understand programming
---

# Basics

Node-RED provides lot of tools and plugins which supports almost everything related to programming.  
 It can be used for APIs, DataBase, IOTIntro to IBM's Node-RED, WebSockets, Emails, Scripting, Image Processing, Cloud computing, edge computing, creating websites and lot more one can think of doing it based on NodeJS. 

Once you have Node-RED set up on your IBM Cloud Account you can create your first flow 

### Steps to Create Flows 

#### Step 1. Add an Inject node 

The Inject node allows you to inject messages into a flow, either by clicking the button on the node, or setting a time interval between injects.

Drag one onto the workspace from the palette.

Open the sidebar \(Ctrl-Space, or via the dropdown menu\) and select the Info tab.

Select the newly added Inject node to see information about its properties and a description of what it does.

![](../.gitbook/assets/image%20%2843%29.png)

#### Step 2. Add a Debug Node 

The Debug node causes any message to be displayed in the Debug sidebar. By default, it just displays the payload of the message, but it is possible to display the entire message object.

![](../.gitbook/assets/image%20%2835%29.png)

#### Step 3. **Wire the two together**

Connect the Inject and Debug nodes together by dragging between the output port of one to the input port of the other.

![](../.gitbook/assets/image%20%2834%29.png)

#### **Step 4. Deploy** 

At this point, the nodes only exist in the editor and must be deployed to the server.

Click the Deploy button. Simple as that.

With the Debug sidebar tab selected, click the Inject button. You should Hello World Selected in the Side Bar. Let’s do something more useful with that.

![](../.gitbook/assets/image%20%2842%29.png)

#### Step 5. **Add a Function node**

The Function node allows you to pass each message though a JavaScript function.

Wire the Function node in between the Inject and Debug nodes. You may need to delete the existing wire \(select it and hit delete on the keyboard\).

Double-click on the Function node to bring up the edit dialog. Copy the follow code into the function field:

```text
var newString = msg.payload.replace("World","Everyone , I hope you enjoy Node Red ");
return {payload : newString};
```

![](../.gitbook/assets/image%20%2822%29.png)



