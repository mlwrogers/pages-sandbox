---
layout: default
title: Send single SMS
parent: SMS
nav_order: 1
---

# Send a single SMS

A simple example of the JSON body used to send a single SMS.

```js

curl --location --request POST 'https://sms.8x8.com/api/v1/subaccounts/<yourSubAccountId>/messages' \
--header 'Authorization: Bearer <yourApiToken>' \
--header 'Content-Type: application/json' \
--data-raw '{
    "clientMessageId": "123xyz",
    "source": "<your_source_SID>",
    "destination": "<the_destination_E.164_number",
    "text": "Show us the value in APIs",
    "encoding": "AUTO"
}'

```