# Renewing Licenses

## Understanding license expiry

Whenever you create a license with validity say 30 days, you will see a property in the license resource named `expiresAt`. It is a read-only, computed property and determines the time when the license will expire.

If the license expiration strategy for a license (or its template) is set to `immediate`, the `expiresAt` property will be populated with the date on which the license will expire starting from the time when the license was created.

If the license expiration strategy for a license (or its template) is set to `delayed`, the `expiresAt` property will be `null` till the license is activated, as the license will start expiring after it is used.

If the license expiration strategy for a license (or its template) is set to `rolling`, the `expiresAt` the property will always be `null` as license expiry is specific to each activation. In this case, you can refer to `expiresAt` property of license activation.

## Renewing license expiry

To renew the license subscription you need to hit the [license renew endpoint](https://api.cryptlex.com/v3/docs#operation/post/v3/licenses/{id}/renew). It extends the license expiry by its validity.

## Renewing license

<mark style="color:green;">`POST`</mark> `https://api.cryptlex.com/v3/licenses/:id/renew`

#### Path Parameters

| Name | Type   | Description                        |
| ---- | ------ | ---------------------------------- |
| id   | string | Unique identifier for the license. |

#### Headers

| Name          | Type   | Description          |
| ------------- | ------ | -------------------- |
| Authorization | string | Bearer access token. |

{% tabs %}
{% tab title="200 " %}
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
  "expiresAt": "2018-07-06T08:49:17.9361143Z",
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
{% endtab %}
{% endtabs %}

