# Automated Emails

Automated emails can be used to automatically send emails to your customers when a specific event is triggered. The following are the supported events:

* `license.created`
* `license.renewed`
* `license.extended`
* `license.expiring-soon`&#x20;
* `license.expired`
* `license.deleted`
* `user.created`
*   `user.reset-password-request`



**NOTE:** Use [webhooks](webhooks.md) instead of automated emails if you have a complex workflow.

## Creating an automated email

You can easily create an automated email through the dashboard. Go to the [automated emails](https://app.cryptlex.com/automated-emails) section in the dashboard and click the add button. An automated email form with the following fields will popup:&#x20;

{% hint style="info" %}
After creating the automated email, make sure you link it with the product.
{% endhint %}

#### **Name**

Name of the automated email.

#### **From Name**

The from name that should appear for the email.

#### **From Email**

The email address to be used for sending the email.

{% hint style="info" %}
The from email address will only be used if you have verified your domain, otherwise, it will default to **noreply@cryptlex.com**.
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

Whether an email should be sent or not, you can use it to disable the automated email.

#### **Custom**

By default, your email body will be automatically wrapped in a responsive HTML email. In case you want to prevent that and use your own branded email, this property can be set to `true`.

## Data placeholders

All the properties of [user](https://api.cryptlex.com/v3/docs#operation/get/v3/users/{id}), [license](https://api.cryptlex.com/v3/docs#operation/get/v3/licenses/{id}) and [product](https://api.cryptlex.com/v3/docs#operation/get/v3/products/{id}) resources can be accessed in the **body** and the **subject** of the automated email. The general syntax is **`resource.propertName`**. Following is a sample automated email body:

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

## Data filters

Data filters can be used to format the date and number fields in automated emails.

### format\_date

Formats date and times.

Input

```
{{ license.expiresAt | format_date: "G" }}
```

Output

```
6/15/2021 1:45:30 PM
```

For more date format specifiers refer to the following: [https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-date-and-time-format-strings#table-of-format-specifiers](https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-date-and-time-format-strings#table-of-format-specifiers)

### format\_number

Formats numbers.

Input

```
{{ license.allowedActivations | format_number: "N" }}
```

Output

```
10.00
```

For other supported filters please refer to the following:

[https://shopify.github.io/liquid/filters/abs/](https://shopify.github.io/liquid/filters/abs/)

## Sending test emails

After you have created the automated email, click the automated email in the automated emails table. On the automated email page, you will find a **`Send Test Email`** button on the right top. You can use this to test your automated email by providing the sample data.

## Verifying email domain

In order for Cryptlex to send emails on your behalf using your **From Email** address, you must verify that you own the domain. This is done by adding a Sending Domain in Cryptlex and verifying the  DNS records shown in the Sending Domain.

If you don’t add the domain verification records, Cryptlex sends emails using **noreply@cryptlex.com** email address. If you want to give your customers a white-label experience, hiding all Cryptlex branding, you must add and verify the sending domain.

### **To verify that a domain belongs to you**

1. On the automated emails page in the dashboard, click on the **`Sending Domains`** button.
2. On the Sending Domains page click on the **`Add`** button to add your domain.
3. Verify the domain by adding the required TXT and CNAME DNS entries.&#x20;
4. After you have added the CNAME and TXT records, click the **`Verify`** button to confirm that all of your records are now valid.

After your domain is verified, leave the CNAME and TXT records in place.

## Automated email event logs

Automated email event logs show information about the emails that were sent by an automated email. You can use automated email event logs to see the status of all the emails that were sent, the email body and even manually resend the email if needed.
