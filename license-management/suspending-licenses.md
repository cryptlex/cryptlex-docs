# Suspending Licenses

Suspending a license will cause **LexActivator** `IsLicenseGenuine()` function to return `LA_SUSPENDED` status code on the user machine, based on which you can take any action in your application.

Allowing the license later will automatically cause **LexActivator** `IsLicenseGenuine()` function to return `LA_OK` status code. User doesn't need to reactivate the license.

## Suspending a license

To suspend a license you need to hit the [license update endpoint](https://api.cryptlex.com/v3/docs#operation/patch/v3/licenses/{id}) and set `suspended` property to `true`.

{% swagger baseUrl="https://api.cryptlex.com" path="/v3/licenses/:id" method="patch" summary="Suspending a license" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="string" %}
Unique identifier for the license.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer access token.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="suspended" type="boolean" %}
Set true to suspend the license.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```javascript
{
  "key": "0A2035-E8A2A3-4D31B7-8FF9C6-81A6CA-539E54",
  "revoked": false,
  "suspended": true,
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
{% endswagger-response %}
{% endswagger %}

