# Creating Licenses

## Creating a license

A license inherits all it's properties from the default license policy attached to it's product. But you may way want to override some properties like `allowedActivations`, `validity`, add some `metadata` etc. You can check out all the properties in the web API [reference page](https://api.cryptlex.com/v3/docs#operation/post/v3/licenses).&#x20;

{% hint style="info" %}
You can also override the default license policy by providing the `licensePolicyId` at the time of creating a license.
{% endhint %}

Following is a sample request which you will usually make to create a license:

{% swagger baseUrl="https://api.cryptlex.com" path="/v3/licenses" method="post" summary="Creating License" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer access token.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="validity" type="number" %}
The duration  after which the license will expire.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="allowedActivations" type="number" %}
Allowed number of activations for the license.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="userId" type="string" %}
Unique identifier for the user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="productId" type="string" %}
Unique identifier for the product.
{% endswagger-parameter %}

{% swagger-response status="201" description="" %}
```javascript
{
  "key": "0A2035-E8A2A3-4D31B7-8FF9C6-81A6CA-539E54",
  "revoked": false,
  "suspended": false,
  "totalActivations": 0,
  "totalDeactivations": 0,
  "validity": 2595000,
  "expirationStrategy": "immediate",
  "fingerprintMatchingStrategy": "fuzzy",
  "allowedActivations": 1,
  "allowedDeactivations": 10,
  "type": "node-locked",
  "allowedFloatingClients": 0,
  "serverSyncGracePeriod": 2595000,
  "serverSyncInterval": 3600,
  "leaseDuration": 0,
  "expiresAt": "2018-06-06T08:49:17.9361143Z",
  "allowVmActivation": true,
  "userLocked": false,
  "productId": "63dfd63e-ed71-4f84-9236-02ee0ddb062c",
  "user": null,
  "allowedCountries": [],
  "disallowedCountries": [],
  "allowedIpAddresses": [],
  "disallowedIpAddresses": [],
  "metadata": [],
  "tags": [],
  "id": "23d9646c-34f5-4d37-adeb-f7f77b927bdb",
  "createdAt": "2018-05-06T08:49:17.9361143Z",
  "updatedAt": "2018-05-06T08:49:17.9361158Z"
}
```
{% endswagger-response %}
{% endswagger %}
