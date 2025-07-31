# Creating Licenses

## Creating a license

A license inherits all it's properties from the default license template attached to its product. But you may way want to override some properties like `allowedActivations`, `subscriptionInterval`, add some `metadata` etc. You can check out all the properties on the web API [reference page](https://api.cryptlex.com/v3/docs#operation/post/v3/licenses).&#x20;

{% hint style="info" %}
You can also override the default license template by providing the `licenseTemplateId` at the time of creating a license.
{% endhint %}

Following is a sample request which you will usually make to create a license:

## Creating License

<mark style="color:green;">`POST`</mark> `https://api.cryptlex.com/v3/licenses`

#### Headers

| Name          | Type   | Description          |
| ------------- | ------ | -------------------- |
| Authorization | string | Bearer access token. |

#### Request Body

| Name                 | Type   | Description                                        |
| -------------------- | ------ | -------------------------------------------------- |
| subscriptionInterval | string | The duration  after which the license will expire. |
| allowedActivations   | number | Allowed number of activations for the license.     |
| userId               | string | Unique identifier for the user.                    |
| productId            | string | Unique identifier for the product.                 |

{% tabs %}
{% tab title="201 " %}
```javascript
{
  "key": "0A2035-E8A2A3-4D31B7-8FF9C6-81A6CA-539E54",
  "revoked": false,
  "suspended": false,
  "totalActivations": 0,
  "totalDeactivations": 0,
  "subscriptionInterval": "P1Y",
  "subscriptionStartTrigger": "creation",
  "fingerprintMatchingStrategy": "fuzzy",
  "allowedActivations": 1,
  "allowedDeactivations": 10,
  "type": "node-locked",
  "allowedFloatingClients": 0,
  "serverSyncGracePeriod": 2595000,
  "serverSyncInterval": 3600,
  "leaseDuration": 0,
  "expiresAt": "2026-05-05T08:49:17.9361143Z",
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
  "createdAt": "2025-05-06T08:49:17.9361143Z",
  "updatedAt": "2025-05-06T08:49:17.9361158Z"
}
```
{% endtab %}
{% endtabs %}
