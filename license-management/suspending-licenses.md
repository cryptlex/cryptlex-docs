# Suspending Licenses

Suspending a license will cause **LexActivator** `IsLicenseGenuine()` function to return `LA_SUSPENDED` status code on the user machine, based on which you can take any action in your application.

Allowing the license later will automatically cause **LexActivator** `IsLicenseGenuine()` function to return `LA_OK` status code. User doesn't need to reactivate the license.

## Suspending a license

To suspend a license you need to hit the [license update endpoint](https://api.cryptlex.com/v3/docs#tag/Licenses/operation/UpdateLicense) and set `suspended` property to `true`.

## Suspending a license

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

| Name      | Type    | Description                      |
| --------- | ------- | -------------------------------- |
| suspended | boolean | Set true to suspend the license. |

{% tabs %}
{% tab title="200 " %}
```javascript
{
  "key": "0A2035-E8A2A3-4D31B7-8FF9C6-81A6CA-539E54",
  "revoked": false,
  "suspended": true,
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
  "expiresAt": "2026-06-05T08:49:17.9361143Z",
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

