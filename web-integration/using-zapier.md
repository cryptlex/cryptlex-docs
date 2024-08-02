# Using Zapier

[Zapier](https://zapier.com/) lets you connect **Cryptlex** with **1000+** cloud apps and automate workflows without writing any server code. You can:

* Automatically send emails to your customers when you generate or renew a license key using Gmail, Mailgun or any other email service.
* Automatically generate licenses on successful payments.
* Automatically renew licenses when your customer renews the subscription.
* Get notified of each activation, license creation, and trial activation through email or slack or any other app.
* Integrate with your CRM and a lot more.

## Zapier Integration

To use Zapier to automate workflows, you need to create a [Personal Access Token](personal-access-tokens.md) which Zapier will use for authorization while invoking Cryptlex web API.

To create an access token for Zapier, go to the [Personal Access Tokens](personal-access-tokens.md) section in the admin portal and create an access token with the following scope (permissions):&#x20;

_`activation:read`, `license:read`, `license:write`, `licensePolicy:read`, `product:read`, `trialActivation:read`, `user:read`, `user:write`, `webhook:read`, `webhook:write`_

Zapier integration is available on invite-only, so please make sure you accept the invitation by clicking the following link:

[https://zapier.com/platform/public-invite/4340/cd16edb4280a1c5985b53917855743bf/](https://zapier.com/platform/public-invite/4340/cd16edb4280a1c5985b53917855743bf/)

## Need more help

In case you need more help with using Zapier, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or contact us through [email](mailto:support@cryptlex.com?Subject=Zapier%20Integration).
