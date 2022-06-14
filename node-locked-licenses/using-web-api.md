# Using Web API

{% hint style="info" %}
We **strongly** recommend using **LexActivator** library for license activation. Web API should **only be used** for license activation, in case LexActivator library is not available for your OS.&#x20;
{% endhint %}

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the 2048-bit RSA public key for the product.

RSA public key is needed to verify the signature of the activation token which you get on activating a license. Product id is the identifier of your product which is to be licensed.

{% hint style="info" %}
In the license policies make sure [`fingerprintMatchingStrategy`](https://docs.cryptlex.com/license-management/license-policies#fingerprint-matching-strategy) is set to `"exact"` as you will be using a custom fingerprint.
{% endhint %}

### Activating the license key

To activate the license in your app using the license key, you need to send a **POST** request to the create activation API endpoint. Refer to the following for API endpoint details:

[https://api.cryptlex.com/v3/docs#tag/Activations/operation/post/v3/activations](https://api.cryptlex.com/v3/docs#tag/Activations/operation/post/v3/activations)

On successful activation, it returns an activation token. The activation token is basically a [JWT](https://jwt.io/) and you can easily verify its signature using any of the JWT libraries available for your language. You can then parse the JWT activation token to get the license details.

### Verifying license activation

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the signature of the JWT activation token using the RSA public key.&#x20;

{% hint style="info" %}
It is recommended to store the JWT activation token in an encrypted form though not required unless you have any sensitive metadata information in the token.
{% endhint %}

You can then parse the JWT activation token to get the license details.

### Syncing license activation

In order to sync the client changes with the server and vice-versa, you need to send a **PATCH** request frequently to the update activation endpoint. You can decide on the update frequency as per your requirement, or use the frequency interval set for the license (available in the JWT activation token). If you choose later you can control it from the dashboard. Refer to the following for API endpoint details:

[https://api.cryptlex.com/v3/docs#tag/Activations/operation/patch/v3/activations/%7Bid%7D](https://api.cryptlex.com/v3/docs#tag/Activations/operation/patch/v3/activations/%7Bid%7D)

### Deleting license activation

In order to delete (deactivate) the activation from the machine, you need to send a **POST** request to the delete activation endpoint. Refer to the following for API endpoint details:

[https://api.cryptlex.com/v3/docs#tag/Activations/operation/post/v3/activations/%7Bid%7D/deactivate](https://api.cryptlex.com/v3/docs#tag/Activations/operation/post/v3/activations/%7Bid%7D/deactivate)
