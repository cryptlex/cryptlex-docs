# Revoking Licenses

Revoking a license will cause **LexActivator** `IsLicenseGenuine()` function to invalidate the local license activation data on the user machine and return `LA_FAIL` status code. Any further attempt to reactivate the license using `ActivateLicense()` will return `LA_E_REVOKED` status code.

Approving the license later will require the user to reactivate the license.

## Revoking a license

To revoke a license you need to hit the [license update endpoint](https://api.cryptlex.com/v3/docs#tag/Licenses/operation/UpdateLicense) and set `revoked` property to `true`.

## Revoking a license

<mark style="color:purple;">`PATCH`</mark> `https://api.cryptlex.com/v3/licenses/:id`

#### Path Parameters

| Name | Type   | Description                        |
| ---- | ------ | ---------------------------------- |
| id   | string | Unique identifier for the license. |

#### Headers

| Name          | Type   | Description          |
| ------------- | ------ | -------------------- |
| Authorization | string | Bearer access token. |

#### Request Body

| Name    | Type    | Description                     |
| ------- | ------- | ------------------------------- |
| revoked | boolean | Set true to revoke the license. |

{% tabs %}
{% tab title="200 " %}
```javascript
{
  "key": "0A2035-E8A2A3-4D31B7-8FF9C6-81A6CA-539E54",
  "revoked": true,
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

