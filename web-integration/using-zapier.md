# Using Zapier

[Zapier](https://zapier.com/) lets you connect **Cryptlex** with **1000+** cloud apps and automate workflows without writing any server code. You can:

* Automatically send emails to your customers when you generate or renew a license key using Gmail, Mailgun or any other email service.
* Automatically generate licenses on successful payments.
* Automatically renew licenses when your customer renews the subscription.
* Get notified of each activation, license creation, and trial activation through email or slack or any other app.
* Integrate with your CRM and lot more

## Zapier Integration

In order to use Zapier to automate workflows, you need to create a "[Personal Access Token](https://app.cryptlex.com/api/personal-access-tokens)" which Zapier will use for authorization while invoking Cryptlex web API.

To create an access token for Zapier, go the "[Personal Access Tokens](https://app.cryptlex.com/api/personal-access-tokens)" section in dashboard and create an access token with following scope \(permissions\): 

_`activation:read`, `license:read`, `license:write`, `licensePolicy:read`, `product:read`, `trialActivation:read`, `user:read`, `user:write`, `webhook:read`, `webhook:write`_

## Need more help

In case you need more help for using Zapier, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Zapier%20Integration).

