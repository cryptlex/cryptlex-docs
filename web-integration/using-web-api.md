# Using Web API

## Order automation 

You can easily automate the order process of your product using Cryptlex Web API. The API can be used with any payment processor. We have examples available on Github  in `Node.js` and `PHP` which you can tailor as per your requirements:

* [Node.js License Generator](https://github.com/cryptlex/nodejs-license-generator)
* [PHP License Generator](https://github.com/cryptlex/php-license-generator)

Following are the steps to automate the process:

### Step 1. Configuring notification API

Each payment processor \(like Paypal, FastSpring, Stripe, 2Checkout, Authorize.net etc.\) has its own notification API. You can configure any server script \(PHP, Node.js etc.\) URL endpoint, which the notification API invokes on successful payment, and passes along other user data. 

So depending on your payment processor you need to set the path for the same. Lets call the script `generate-license.php`. So the sample path would look like:

```text
https://yourserver.com/generate-license.php
```

### Step 2. Generate license key using notification script

When your `generate-license.php` is invoked by your payment processor, you get access to all the payment and customer related data which your payment processor passes after the successful payment. 

The `generate-license.php`  generates license key for your customer and returns it to your payment processor. It also creates a user in Cryptlex using the customer details present in the request.

### Step 3. Email license key to your customer

After the license key is generated, either your payment processor will send an email or you can create an [email template](../email-templates.md) to send the license key to your customer. 

Alternatively, you can also use [webhooks](../webhooks.md) to send the email by writing a simple mail script or by using any third party mailing service like SendGrid, MailGun etc.

## Need more help?

In case you need more help for automating your order process we'll be glad to help you. You can either post your questions on our [support forum](https://forums.cryptlex.com) or contact us through [email](mailto:support@cryptlex.com?Subject=Order%20Automation).

