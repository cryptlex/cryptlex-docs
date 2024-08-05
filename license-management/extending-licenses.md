# Extending Licenses

## Extending license expiry

Renewing a license extends the license expiry by it's validity. In case you want to extend the license expiry by some other duration you need to hit the [license extend endpoint](https://api.cryptlex.com/v3/docs#tag/Licenses/operation/ExtendLicense). It extends the license expiry by provided extension length.

## Extending license

<mark style="color:green;">`POST`</mark> `https://api.cryptlex.com/v3/licenses/:id/extend`

#### Path Parameters

| Name | Type   | Description                        |
| ---- | ------ | ---------------------------------- |
| id   | string | Unique identifier for the license. |

#### Headers

| Name          | Type   | Description          |
| ------------- | ------ | -------------------- |
| Authorization | string | Bearer access token. |

#### Request Body

| Name            | Type   | Description                                              |
| --------------- | ------ | -------------------------------------------------------- |
| extensionLength | string | License extension duration to extend the license expiry. |

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

