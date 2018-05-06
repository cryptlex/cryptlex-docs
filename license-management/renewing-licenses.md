---
description: >-
  When your customer renews the subscription, you will need to renew the license
  too.
---

# Renewing Licenses

## Understanding License Expiry

Whenever you create a license with validity say 30 days, you will see a property in the license resource named `expiresAt`. It is a read only, computed property and determines when license will expire.

If the license expiration strategy for license \(or it's policy\) is set to `immediate`, this property will be populated with the date on which license will expire starting from the time when license was created.

If the license expiration strategy for license \(or it's policy\) is set to `delayed`, this property will be `null` unless license is activated, as license will start expiring after it is used.

If the license expiration strategy for license \(or it's policy\) is set to `rolling`, this property will always be `null` as license expiry is specific to each activation. In this case you can refer to `expiresAt` property of license activation.

## Renewing License Expiry

To renew the license subscription you need to hit the [license renew endpoint](https://api.cryptlex.com/v3/docs#operation/V3LicensesByIdRenewPost). It extends the license expiry by it's validity.

{% api-method method="post" host="https://api.cryptlex.com" path="/v3/licenses/:id/renew" %}
{% api-method-summary %}
Renewing License
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=false %}
Unique identifier for the license.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer access token.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



