# LexFloatServer API Endpoints

LexFloatServer provides several API endpoints for retrieving information related to its status, license details, leased floating licenses, meter attributes, and feature entitlements.

## Getting server stats

LexFloatServer exposes a stats API endpoint that can be used to get the current stats of the server.

### Gets the server stats

<mark style="color:blue;">`GET`</mark> `http://localhost:8090/api/server/stats`

Gets the current server stats

{% tabs %}
{% tab title="200 " %}
<pre class="language-javascript"><code class="lang-javascript"><strong>{
</strong>    "leaseDuration": 60,
    "maxOfflineLeaseDuration": 30,
    "allowedFloatingClients": 10,
    "allowedOfflineFloatingClients": 0,
    "totalFloatingClients": 5,
    "totalOfflineFloatingClients": 0,
    "leasingStrategy": "per-machine",
    "version": "4.13.3",
    "status": "ok",
    "expiresAt": 1751178927,
    "serverSyncGracePeriodExpiresAt": 0
}
</code></pre>
{% endtab %}
{% endtabs %}

## Getting server license info

LexFloatServer exposes a license info API endpoint that can be used to get the information related to the license used to activate the LexFloatServer.

### Gets the license info

<mark style="color:blue;">`GET`</mark> `http://localhost:8090/api/server/license-info`

Gets the license info of the license used to activate the LexFloatServer

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
  "key": "280D2B-B48A03-406BBC-2EEE4A-C20FB3-749630",
  "allowedFloatingClients": 10,
  "createdAt": 1680518500,
  "activatedAt": 1680518506,
  "expiresAt": 1681814506,
  "serverSyncGracePeriodExpiresAt": 1680775357,
  "activationMode": {
    "initial": "online",
    "current": "online"
  },
  "user": {
    "name": "John Doe",
    "email": "johndoe@example.com",
    "company": "My Example Company"
  },
  "organization": null
}
```
{% endtab %}
{% endtabs %}

## Getting the list of floating licenses

LexFloatServer exposes a floating-licenses API endpoint that can be used to get the leased floating licenses.

### Gets the list of floating licenses

<mark style="color:blue;">`GET`</mark> `http://localhost:8090/api/floating-licenses`

Gets the current server stats

{% tabs %}
{% tab title="200 " %}
```javascript
[
  {
    "id": "3a13465d984ef1f4b21b2117e0b3f591116f6b027fa8a19f332fbc43651f3d2c",
    "ip": "127.0.0.1",
    "os": "macos",
    "osVersion": "10.14",
    "hostname": "MB-Pro.local",
    "clientVersion": "4.0.0",
    "expiresAt": 1545019266,
    "updatedAt": 1545019236,
    "createdAt": 1545019236,
    "metadata": [
      {
        "key": "name",
        "value": "John Doe"
      }
    ]
  }
]
```
{% endtab %}
{% endtabs %}

## Getting server license meter attributes

LexFloatServer exposes a license meter attributes API endpoint that can be used to get the list of all the meter attributes of the license used to activate the LexFloatServer.

### Gets the list of license meter attributes

<mark style="color:blue;">`GET`</mark> `http://localhost:8090/api/server/license-meter-attributes`

Gets the list of meter attributes of the license used to activate the LexFloatServer

{% tabs %}
{% tab title="200: OK " %}
<pre class="language-javascript"><code class="lang-javascript">[
  {
    "id": "string",
    "name": "string",
<strong>    "allowedUses": 0,
</strong>    "totalUses": 0,
    "grossUses": 0,  
  }
]
</code></pre>
{% endtab %}
{% endtabs %}

## Getting server license feature entitlements

LexFloatServer exposes a feature entitlement API endpoint that can be used to get the list of all the feature entitlements associated with the license used to activate the LexFloatServer.

### Gets the list of feature entitlements

`GET` `http://localhost:8090/api/server/feature-entitlements`

Gets the list of feature entitlements associated with the license used to activate the LexFloatServer.

{% tabs %}
{% tab title="200: OK " %}
```javascript
[
  {
    "featureName": "string",
    "featureDisplayName": "string",
    "value": "string",
  }
]
```
{% endtab %}
{% endtabs %}
