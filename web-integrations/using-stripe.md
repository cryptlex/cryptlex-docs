# Using Stripe

This guide walks you through integrating Stripe with Cryptlex to automate license creation and license subscription renewals.

### Prerequisites

1. Complete the Cryptlex [Quick Start Guide](https://docs.cryptlex.com/#quick-start) to set up your product and license templates.
2. Deploy the Stripe-Cryptlex integration script using one of the following options:
   * **Self-hosted**: Follow our [deployment guide](https://github.com/cryptlex/third-party-integrations/tree/main/stripe) to run the integration on your infrastructure.
   * **Cryptlex-hosted**: Let Cryptlex host the integration for a nominal fee. Contact [support](mailto:support@cryptlex.com) to request managed hosting.

### Step 1: Set Up Products in Stripe

In your Stripe Dashboard:

1. Navigate to **Products** and create your desired product(s).
2. Pass the Cryptlex `productId` to the integration script to enable license creation and subscription renewal for the selected product.

### Step 2: Configure Webhooks

1. In your Stripe Dashboard, go to **Developers > Webhooks**.
2. Click **Add Endpoint**, and enter the URL where your integration script is hosted.
3. Select one of the following events to listen for:
   * `checkout.session.completed` – Triggers license creation after successful checkout.
   * `invoice.paid` – Triggers license creation and also handles subscription renewals.
4. Retrieve the **signing secret** and provide it to your integration script for webhook verification.

### What Happens Next

Once the integration is active:

* New licenses are automatically created after successful Stripe payments.
* A user is created in Cryptlex using the customer's name and email from Stripe.
* Licenses are automatically renewed in Cryptlex when the corresponding Stripe subscription renews.

{% hint style="info" %}
Each license includes a metadata field named `SUBSCRIPTION_ID_KEY` that stores the Stripe subscription ID. Do not modify this value.
{% endhint %}

## Need more help?

In case you need more help with using Stripe, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com/) or contact us through [email](mailto:support@cryptlex.com).
