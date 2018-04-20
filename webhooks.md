# Webhooks

## When to use webhooks

The most common use-case of webhooks is to automate the communication between Cryptlex and other 3rd party apps asynchronously. You might use webhooks to:

* Email a license key to your customer after a successful purchase.
* Email your customer when the license expires.
* Renew subscription licenses when your customer makes the payment.
* Get notified through email or chatting apps like slack when any user activates the trial or license.
* Any other integration your business needs.

## Creating a webhook

You can easily create a webhook through dashboard. Go to the [webhooks](https://app.cryptlex.com/webhooks) section in the dashboard and click the add the button. A webhook form with following fields will popup: 

* **URL** - the endpoint which will receive the HTTP POST payload
* **Token** - the secret which will be used to sign the payload using **HMAC256** algorithm
* **Events** - the list of events you want to subscribe
* **Active** - whether webhook is active not, you can use it to disable a webhook

## Webhook payload

Each event type has a specific payload format with the relevant event information. Additionally, the signature generated using **HMAC256** algorithm is included in **"webhook-signature"** header. A typical payload will have a following structure:

```javascript
POST /payload HTTP/1.1
Content-Type:	application/json; charset=utf-8
Content-Length:	661
Webhook-Signature:	Bb3jMWkC1DOqEv5fAOsqwkKH7r57w9o8fZ3Jg72lNk0=

{
  "event": "license.created",
  "data": {
    "key": "D08B53-C564F8-463EA5-F16A15-E35D6E-D2559B",
    ...
  },
  "triggeredAt": "2018-04-20T13:11:34.6926949Z"
}
```



