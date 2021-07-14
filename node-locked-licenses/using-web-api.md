# Using Web API

{% hint style="info" %}
We **strongly** recommend using LexActivator library for license activation. Web API should **only be used** for license activation, in case LexActivator library is not available for your OS e.g. Android and iOS. 
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

{% api-method method="post" host="https://api.cryptlex.com" path="/v3/activations" %}
{% api-method-summary %}
Create a license activation
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="key" type="string" required=true %}
License key to activate the license.
{% endapi-method-parameter %}

{% api-method-parameter name="hostname" type="string" required=true %}
Name of the host machine.
{% endapi-method-parameter %}

{% api-method-parameter name="os" type="string" required=true %}
Name of the operating system.
{% endapi-method-parameter %}

{% api-method-parameter name="osVersion" type="string" required=false %}
Version of the operating system.
{% endapi-method-parameter %}

{% api-method-parameter name="fingerprint" type="string" required=true %}
Fingerprint of the machine.
{% endapi-method-parameter %}

{% api-method-parameter name="vmName" type="string" required=false %}
Name of the virtual machine.
{% endapi-method-parameter %}

{% api-method-parameter name="metadata" type="array" required=false %}
List of metadata key/value pairs.
{% endapi-method-parameter %}

{% api-method-parameter name="appVersion" type="string" required=true %}
Version of the application.
{% endapi-method-parameter %}

{% api-method-parameter name="userHash" type="string" required=true %}
Hash of the machine user name.
{% endapi-method-parameter %}

{% api-method-parameter name="productId" type="string" required=true %}
Unique identifier for the product.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "activationToken": "string"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

On successful activation it returns an activation token. Activation token is basically a [JWT](https://jwt.io/) and you can easily verify it's signature using any of the JWT libraries available for your language. You can then parse the JWT activation token to get the license details.

### Verifying license activation

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the signature of the JWT activation token using the RSA public key. 

{% hint style="info" %}
It is recommended to store the JWT activation token in an encrypted form though not required unless you have any sensitive metadata information in the token.
{% endhint %}

You can then parse the JWT activation token to get the license details.

### Syncing license activation

In order to sync the client changes with the server and vice-versa you need to frequently sent an update request. You can decide on the update frequency as per your requirement, or use the frequency interval set for the license \(available in JWT activation token\). If you choose latter you can control it from dashboard.

{% api-method method="patch" host="https://api.cryptlex.com" path="/v3/activations/:id" %}
{% api-method-summary %}
Updating a license activation
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Unique identifier for the activation.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="key" type="string" required=true %}
License key to activate the license.
{% endapi-method-parameter %}

{% api-method-parameter name="hostname" type="string" required=true %}
Name of the host machine.
{% endapi-method-parameter %}

{% api-method-parameter name="os" type="string" required=true %}
Name of the operating system.
{% endapi-method-parameter %}

{% api-method-parameter name="osVersion" type="string" required=false %}
Version of the operating system.
{% endapi-method-parameter %}

{% api-method-parameter name="fingerprint" type="string" required=true %}
Fingerprint of the machine.
{% endapi-method-parameter %}

{% api-method-parameter name="vmName" type="string" required=false %}
Name of the virtual machine.
{% endapi-method-parameter %}

{% api-method-parameter name="metadata" type="array" required=false %}
List of metadata key/value pairs.
{% endapi-method-parameter %}

{% api-method-parameter name="appVersion" type="string" required=true %}
Version of the application.
{% endapi-method-parameter %}

{% api-method-parameter name="userHash" type="string" required=true %}
Hash of the machine user name.
{% endapi-method-parameter %}

{% api-method-parameter name="productId" type="string" required=true %}
Unique identifier for the product.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
  "activationToken": "string"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

