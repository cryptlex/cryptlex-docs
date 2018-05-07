---
description: >-
  You can directly use the web API to implement licensing in your app. We
  recommend using web API only for platforms where LexActivator is not available
  like Android, IOS, OpenBSD etc.
---

# Using Web API

## Activating the License Key

Following is a sample request which creates a license activation:

{% api-method method="post" host="https://api.cryptlex.com" path="/v3/activations" %}
{% api-method-summary %}
Create a License Activation
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

## Updating the License Activation

In order to sync the client changes with the server and vice-versa you need to frequently sent the update request. You can decide on the update frequency as per your requirement.

{% api-method method="patch" host="https://api.cryptlex.com" path="/v3/activations/:id" %}
{% api-method-summary %}
Updating a License Activation
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

