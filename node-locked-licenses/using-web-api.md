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

To activate the license in your app using the license key, you need to send a POST request to the [/v3/activations](https://api.cryptlex.com/v3/docs#operation/post/v3/activations) API endpoint. Following is a sample request which creates a license activation:

{% swagger baseUrl="https://api.cryptlex.com" path="/v3/activations" method="post" summary="Create a license activation" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="key" type="string" %}
License key to activate the license.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="hostname" type="string" %}
Name of the host machine.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="os" type="string" %}
Name of the operating system.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="osVersion" type="string" %}
Version of the operating system.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fingerprint" type="string" %}
Fingerprint of the machine.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="vmName" type="string" %}
Name of the virtual machine.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="metadata" type="array" %}
List of metadata key/value pairs.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="appVersion" type="string" %}
Version of the application.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="userHash" type="string" %}
Hash of the machine user name.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="productId" type="string" %}
Unique identifier for the product.
{% endswagger-parameter %}

{% swagger-response status="201" description="" %}
```javascript
{
  "activationToken": "string"
}
```
{% endswagger-response %}
{% endswagger %}

On successful activation it returns an activation token. Activation token is basically a [JWT](https://jwt.io) and you can easily verify it's signature using any of the JWT libraries available for your language. You can then parse the JWT activation token to get the license details.

### Verifying license activation

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the signature of the JWT activation token using the RSA public key.&#x20;

{% hint style="info" %}
It is recommended to store the JWT activation token in an encrypted form though not required unless you have any sensitive metadata information in the token.
{% endhint %}

You can then parse the JWT activation token to get the license details.

### Syncing license activation

In order to sync the client changes with the server and vice-versa you need to frequently sent an update request. You can decide on the update frequency as per your requirement, or use the frequency interval set for the license (available in JWT activation token). If you choose latter you can control it from dashboard.

{% swagger baseUrl="https://api.cryptlex.com" path="/v3/activations/:id" method="patch" summary="Updating a license activation" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" %}
Unique identifier for the activation.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="key" type="string" %}
License key to activate the license.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="hostname" type="string" %}
Name of the host machine.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="os" type="string" %}
Name of the operating system.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="osVersion" type="string" %}
Version of the operating system.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fingerprint" type="string" %}
Fingerprint of the machine.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="vmName" type="string" %}
Name of the virtual machine.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="metadata" type="array" %}
List of metadata key/value pairs.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="appVersion" type="string" %}
Version of the application.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="userHash" type="string" %}
Hash of the machine user name.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="productId" type="string" %}
Unique identifier for the product.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "activationToken": "string"
}
```
{% endswagger-response %}
{% endswagger %}
