---
layout: default
title: Customer Care WhatsApp Service
parent: ChatApps
---

# Customer Care WhatsApp Service

Credit: Contributed by [Filipe Leitao.](https://github.com/fleitao/)
{: .fs-2 }

This short guide will help you to build a simple node.js app that simulates an airline customer care service using WhatsApp along with a _(simulated)_ chat bot.  

## See It In Action

Dive right in and watch this short demonstration before trying it out for yourself!

<iframe width="560" height="315" src="https://www.youtube.com/embed/fgznkruPAtw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Build it yourself** 👇

## What You'll Need

* [ngrok](https://ngrok.com/) _(optional)_
* [8x8 Connect Account](https://connect.8x8.com/login)
* 8x8 WhatsApp Sandbox access
* [node.js](https://nodejs.org/)

## Getting Started

### ngrok

Skip this step if your are working on a VPS with public IP address.
If you're using your own machine to host the webhook server, download ngrok if you have not already. It is a handy tool that provides an external URL to map to localhost:port.
The application defaults to port 8089, so launch ngrok http mapping to port 8089:

`$ ngrok http 8089`

Be sure to copy the forwarding ngrok url, we’ll need that later to configure the webhook.

### 8x8 Connect account

1. Create a 8x8 Connect Account ([here](https://connect.8x8.com/login/signup))
2. Reach out to your 8x8 Account Manager for testing credit and 8x8 WhatsApp Sandbox access
3. Once in, fetch your credentials (AccountID, SubAccountID and API Key) directly from the [8x8 Connect API Key dashboard](https://connect.8x8.com/messaging/api-keys)

### node.js

For this app I'm using [axios](https://axios-http.com/) to execute HTTP requests and [express](https://expressjs.com/) to create the webapp/webhook that will be listening to incoming messages.
You can fetch and install those dependencies by executing the following on the root directory of the app:

`npm install axios`

`npm install express`


## The Basics

Before executing the scripts there are two things you'll need to take care first.

### Setup connect.json

Add your 8x8 Connect credentials to connect.json. Fetch your credentials from [8x8 Connect API Key dashboard](https://connect.8x8.com/messaging/api-keys) and edit `connect.json` by replacing the defaults with yours:

 ```
 {
    "accountID": "your_accountID_here",
    "subAccountID": "your_subaccountID_here",
    "apiToken": "your_apikey_here",
    "number": "your_smsnumber_here"
}
 ```

### Setup the webhook

So that the messages sent to your 8x8 number reach your webhook we need to configure that first. If you are using your own VPS simply use your IP address + `/whatsapp` + `:8089`. If you are using ngrok simply take the url provided when you launched the service and add '/whatsapp'

`$ node 8x8-update-chatapps-webhook.js http://ngrok-url-from-your-machine/whatsapp`

## Light It Up

You should be ready to try the app now. Lets test this out in the following order:

1. Start the webhook listener app
2. Use your phone's WhatsApp application to send a message to your 8x8 Sandbox Number starting with `hello airline`.
3. You should see the message coming into your bash prompt and simultaneously you'll see the "bot" replying.
4. Reply back with one of the options provided to check what other automated messages the script is sending.
5. Use the script to send a whatsapp message to your phone simulating a real-human agent jumping into the conversation.

**Please Note:** if you are using the 8x8 WhatsApp Sandbox you might have to open the WhatsApp 24h support window. Please reach out to your 8x8 Account Manager for instructions on how to do this and what is the number to use.

### Start the webhook

`$ node airline-receive-whatsapp.js`

### Text your Sandbox/WhatsApp number

Send a message to your sandbox or WhatsApp number that starts with `hello airline`. You should see the message coming into your bash prompt and as response you should see the "bot" replying with the following menu:

```
✈️ Airline ChatBot 🤖
How ya! 👋
I am Airline's chatbot 🤖 and I'm here to help.
If needed, I can also put you in contact with a customer support agent (real human 👩).
Are you having troubles with your booking ✈️, ticket 🎟️, or anything else I could help you with?
```

### Send a message to your phone

At any time you can simulate a real human agent jumping into the conversation by executing the send message script:

`$ node airline-send-whatsapp.js +447771649919 "Hi there, agent Smith here, how can I help you`

## Extra Resources

The node.js scripts used for this demonstration may be accessed from Filipe's Github repository [here.](https://github.com/fleitao/the-8x8-collection/tree/main/whatsapp-airline-simple-2-way)