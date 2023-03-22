---
title: "Learn How to automate slack message with google appscript free"
slug: "how-to-automate-slack-message-with-google-appscript-free"
date: 2023-03-22T23:14:11+05:30
image : "https://user-images.githubusercontent.com/26689210/227001708-fa12952f-c97e-4153-934c-641cbb5b5bac.png"
# author
author : ["Ronak Vanpariya"]
# categories
categories: ["Technology"]
tags: ["tools", "google appsscript", "slack", "automation"]
# meta description
description: "Learn How to automate slack message with google appscript free"
keywords: ["slack", "slack automation", "automate slack message", "automation with google appsscript"]
# save as draft
draft: false
---

> This tutorial describes how to automate the slack messages with google apps script for free of cost.

This tutorial describes how to automate the slack messages with google apps script for free of cost. Yes you read it right, We do not need the server for the webhooks of slack.

## What is the webhook of slack?
Slack Webhook allows users to send data to slack easily from outside APIs or resources. This can be a very useful feature to make a better notification system. You do not need to go through the email for important notification.


## Create a google apps script project

`googleappscript.gs`
```javascript
const sendMessageToSlack = () => {
    const WEBHOOK_URL = “YOUR webhook from slack”
    var payload = {
     "channel" : "#watercooler",
     "username" : "",
     "icon_url" : “”,
     "text" : `Hello Team :memo: This is the important Updates, *Sales Team* please have a look :face_with_monocle:`,
     "attachments": [{
       // "text": `:memo: ${quotes[quoteNumber].quote}`,
       "text": “ADD any text”,
       "footer": "<”YOUR_GOOGLE_SHEET_URL”|edit script>",
       "mrkdwn_in": ["text"]
     }]
   }
  var options = {
   "method" : "post",
   "contentType" : "application/json",
   "payload" : JSON.stringify(payload)
 };
 var results = UrlFetchApp.fetch( WEBHOOK_URL , options);
 }
```




## Set triggers
 
I prefer my notification code daily in the morning, You can adjust your time by changing drop down.

![How to set triggers in Google AppScript](https://user-images.githubusercontent.com/26689210/227000843-85752bed-20ba-4125-85b8-0e193397f8e9.png)


## Test integration
Test google apps script function by clicking the run button. Please select appropriate function to run.

![How to run function in Google AppScript](https://user-images.githubusercontent.com/26689210/227000910-781c5e32-dc84-49ff-9939-d3145c356444.png)

## Creativity
You can be creative with your code as much as you can. Few ideas for slack notification.
Create downtime monitor
Track domains and subscription monitor
Track credit card due dates
Track some specific rules by own

This list is very long and it is free to use. You do not need to pay for sass tool once you developed your desired solution.



{{< footer-donation >}}