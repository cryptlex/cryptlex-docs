# Using FastSpring

This tutorial will guide you through setting up FastSpring integration with Cryptlex for automated license management. It supports both one-time purchases and subscriptions. For subscriptions, it handles renewals, suspensions, and deletions based on the corresponding subscription events.

## Prerequisites

1. Follow the Cryptlex quick start in the [documentation](https://docs.cryptlex.com/#quick-start).
2. Deployment of the integration script by either:
   * **Self hosting:** Follow the [deployment guide](https://github.com/cryptlex/third-party-integrations/tree/main/fastspring) to set up and configure the integration on your own infrastructure.
   * **Cryptlex-hosted deployment:** Opt for Cryptlex’s managed hosting service for a nominal fee.

### Step 1: Configure FastSpring Products

* Go to the "Catalog" section in FastSpring dashboard.
* Add these custom attributes to your “Product” or “Subscription”:
  * `cryptlex_product_id`
  * `cryptlex_license_template_id`
  * `cryptlex_subscription_interval` (Optional - Use this to override the subscription interval defined in the license template)

{% hint style="info" %}
For multiple products, ensure each has unique custom attributes.
{% endhint %}

### Step 2: Set Up Webhooks

* Navigate to "Developer Tools" > "Webhooks" in FastSpring.
* Click "ADD WEBHOOK" and enable "webhook expansion".
* Configure the URL Endpoint by specifying the URL of the deployed integration script.
* Configure a secret in the HMAC SHA-256 Secret field. This secret must also be passed to the integration script to ensure secure verification of webhook requests.
* Configure the webhook to send specific or all available events, depending on your use case:
  * **`order.completed`** - Creates a new license.
  * **`subscription.charge.completed`** - [Renews](https://docs.cryptlex.com/license-management/license-subscriptions#renewing-a-subscription) the associated license.
  * **`subscription.payment.overdue`** - [Suspends](https://docs.cryptlex.com/license-management/suspending-licenses) the associated license.
  * **`subscription.deactivated`** - Deletes the license.

### What Happens Next

Once the integration is active:

* New licenses are automatically created upon order completion.
* New users are created in Cryptlex using the customer's email and name present in the checkout and are automatically linked to the corresponding license.
* Licenses are automatically renewed in Cryptlex when the corresponding FastSpring subscription renews.

## Need more help?

In case you need more help with using FastSpring, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com/) or contact us through [email](mailto:support@cryptlex.com).
