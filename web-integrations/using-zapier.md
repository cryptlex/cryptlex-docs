# Using Zapier

[Zapier](https://zapier.com/) lets you connect **Cryptlex** with **1000+** cloud apps and automate workflows without writing any server code. You can:

* Automatically send emails to your customers when you generate or renew a license key using Gmail, Mailgun or any other email service.
* Automatically generate licenses on successful payments.
* Automatically renew licenses when your customer renews the subscription.
* Get notified of each activation, license creation, and trial activation through email or slack or any other app.
* Integrate with your CRM and a lot more.

## Zapier Integration

To use Zapier to automate workflows, you need to create a [Personal Access Token](broken-reference) which Zapier will use for authorization while invoking Cryptlex web API.

To create an access token for Zapier, go to the [Personal Access Tokens](https://app.cryptlex.com/developer/access-tokens) section in the admin portal and create an access token with the following scope (permissions):&#x20;

_`activation:read`, `license:read`, `license:write`, `licenseTemplate:read`, `product:read`, `trialActivation:read`, `user:read`, `user:write`,_ `organization:read`, `organization:write`, _`webhook:read`, `webhook:write`_

{% hint style="info" %}
To add metadata to a license, ensure the corresponding metadata key is first defined in the license template.
{% endhint %}

Zapier integration is available on invite-only, so please make sure you accept the invitation by clicking the following link:

[https://zapier.com/developer/public-invite/4340/7305829489e08628e45c0a069e6dc275/](https://zapier.com/developer/public-invite/4340/7305829489e08628e45c0a069e6dc275/)

## Need more help?

In case you need more help with using [Zapier](https://zapier.com/), we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or contact us through [email](mailto:support@cryptlex.com?Subject=Zapier%20Integration).
