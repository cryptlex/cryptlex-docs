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

{% hint style="info" %}
After creating the email template, make sure you link it with product.
{% endhint %}

#### **Name**

Name of the email template.

#### **From Name**

The from name which should appear for the email.

#### **From Email**

The email address to be used for sending the email.

{% hint style="info" %}
The from email address will only be used if you have verified your domain, otherwise it will default to **noreply@cryptlex.com**.
{% endhint %}

#### Subject

The subject of the email. This can contain data placeholders too.

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

All the properties of [user](https://api.cryptlex.com/v3/docs#operation/get/v3/users/{id}), [license](https://api.cryptlex.com/v3/docs#operation/get/v3/licenses/{id}) and [product](https://api.cryptlex.com/v3/docs#operation/get/v3/products/{id}) resources can be accessed in the **body** and the **subject** of the email template. The general syntax is **`resource.propertName`**. Following is a sample email template body:

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

## Verifying email domain

In order for Cryptlex to send emails on your behalf using your **From Email** address, you must verify that you own the domain. This is done by adding a TXT record \(a domain verification record\) to your DNS server that Cryptlex will check. The domain verification record is unique for each Cryptlex account.

If you don’t add the domain verification record, Cryptlex sends emails using **noreply@cryptlex.com** email address. If you want to give your customers a white label experience, hiding all Cryptlex branding, you must add this record.

### **To verify that a domain belongs to you**

1. Select the email template in the dashboard and click on the **`Verify Email Domain`** button.
2. Edit your domain's DNS settings and add this TXT record:

   | Type | Name | Value | TTL |
   | :--- | :--- | :--- | :--- |
   | TXT | &lt;mydomain.com&gt; | &lt;your unique value found in the verify email domain dialog&gt; | 3600 or use default |

3. After you add the TXT record, click the **`Verify`** button to confirm that all of your records are now valid.

After your domain is verified, leave the domain verification TXT record in-place.

### Setting up an SPF record

Sender Policy Framework \(SPF\) is a domain level email authorization protocol that allows you to declare which IP addresses are allowed to send email as if it originated from your domain.

When an email client receives a message, it performs an SPF check on the sending domain to verify that the email came from who it says it did. If this check fails, or there isn't a DNS record that says that Cryptlex is a permitted sender, some receivers might consider that email spam or a phishing attempt, and flag it as untrustworthy or not display it to your customers at all.

To create or edit an SPF record to reference Cryptlex, edit your domain's DNS settings to add a TXT record. The steps vary depending on your domain registrar. Cryptlex recommends using the following SPF record:

```text
v=spf1 include:mail.cryptlex.com ?all
```

If you've already set up an SPF record for another purpose, you can simply add a reference of Cryptlex to it. The SPF specification requires that you only have one SPF record on your domain, if you have multiple records, it may cause issues, and cause rejections of your email.

For example, instead of having two separate records, such as `v=spf1 include:_spf.google.com ~all` and `v=spf1 include:mail.cryptlex.com ~all`, you can combine them into one, like this:

```text
v=spf1 include:_spf.google.com include:mail.cryptlex.com ~all
```

