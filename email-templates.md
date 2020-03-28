# Email Templates

Email templates can be used to automatically send emails to your customers when a specific event is triggered. Following are the supported events:

* `license.created`
* `license.renewed`
* `license.extended`
* `license.expiring-soon` \(triggered **three** days before license expiry date\)
* `license.expired`

**NOTE:** Use [webhooks](webhooks.md) instead of email templates if you have a complex workflow.

## Creating an email template

You can easily create an email template through dashboard. Go to the [email templates](https://app.cryptlex.com/email-templates) section in the dashboard and click the add the button. An email template form with following fields will popup: 

#### **Name**

Name of the email template.

#### **From Name**

The from name which should appear for the email.

#### **From Email**

The email address to be used for sending the email.

{% hint style="info" %}
By default this is set to **noreply@cryptlex.com**. The can be set to a custom email address in case you are subscribed to `SMALL BUSINESS` or a higher plan.
{% endhint %}

#### Subject

The subject of the email.

#### **ReplyTo**

Reply to address for the email. We recommend setting this to your support email.

#### **Body**

The body of the email. You can use HTML for formatting.

#### **Event**

The event to trigger the email.

#### **Enabled**

Whether email should be sent or not, you can use it to disable the email template.

#### **Custom**

By default your email body will be automatically wrapped in a responsive HTML email. In case you want to prevent that and use your own branded email, this property can be set to `true`.

## Data placeholders

All the properties of [user](https://api.cryptlex.com/v3/docs#operation/get/v3/users/{id}), [license](https://api.cryptlex.com/v3/docs#operation/get/v3/licenses/{id}) and [product](https://api.cryptlex.com/v3/docs#operation/get/v3/products/{id}) resources can be accessed in the body of the email template. The general syntax is **`resource.propertName`**. Following is a sample email template body:

```markup
<p>Dear {{user.firstName}},</p>

<p>Thank you for ordering {{product.displayName}}.</p>

<p>Your license key for the {{product.displayName}} is:</p> 

<p><b>{{license.key}}</b></p>

<p>You can use this license key to activate {{product.displayName}} on 
<b>{{license.allowedActivations}}</b> device(s).

<p>For any queries or issues you can contact us at 
<a href="mailto:support@mycompany.com">support@mycompany.com</a> and we will 
assist you promptly.</p>

<p>Best Regards,<br>
The MyCompany HelpDesk</p>
```

## Sending test emails

After you have created the email template, click the email template in the email templates table. On the email template page you will find a **`Send Test Email`** button on the right top. You can use this to test your email template by providing the sample data.

