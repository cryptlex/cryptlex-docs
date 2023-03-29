---
description: >-
  Webhooks are basically user defined HTTP callbacks which are triggered by
  specific events.
---

# Webhooks

## When to use webhooks

The most common use case of webhooks is to automate the communication between Cryptlex and other 3rd party apps asynchronously. You might use webhooks to:

* Email a license key to your customer after a successful purchase.
* Email your customer when the license expires.
* Renew subscription licenses when your customer makes the payment.
* Get notified through email or chat apps like slack when any user activates the trial or license.
* Any other integration your business needs.

## Creating a webhook

You can easily create a webhook through the dashboard. Go to the [webhooks](https://app.cryptlex.com/webhooks) section in the dashboard and click the add button. A webhook form with the following fields will popup:&#x20;

#### **Name**

Name for the webhook.

#### **URL**

The endpoint which will receive the HTTP POST payload.

#### **Token**

The token is a secret that will be used to sign the payload using the **HMAC256** algorithm.

#### Events

The list of events which trigger the POST request.

#### **Active**

If unchecked, the webhook will be disabled and will not send a POST request on the defined events.

## Webhook payload

Each event type has a specific payload format with relevant event information. Additionally, the signature generated using the **HMAC256** algorithm is included in the **"Webhook-Signature"** header. A typical payload will have the following structure:

```javascript
POST /webhook-endpoint HTTP/1.1
Content-Type: application/json; charset=utf-8
Content-Length: 661
Webhook-Signature: Bb3jMWkC1DOqEv5fAOsqwkKH7r57w9o8fZ3Jg72lNk0=

{
  "event": "license.created",
  "data": {
    "key": "D08B53-C564F8-463EA5-F16A15-E35D6E-D2559B",
    ...
  },
  "triggeredAt": "2018-04-20T13:11:34.6926949Z"
}
```

## Webhook event logs

Webhook event logs show information about POST requests that were made when the webhook was triggered. You can use webhook event logs to see the status code returned by your endpoint when it received the webhook request, when the request was sent and when it was received, and the reason why a retry occurred for the request.
