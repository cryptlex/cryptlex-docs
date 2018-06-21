---
description: >-
  Each release gets it's own unique download link which is secured using license
  key or access token.
---

# Distributing Releases

## Downloading a release

In order to download the release, the release url must contain license key as  `key` query parameter or access token in the header.

```bash
# using license key
curl -O -J -L https://releases.cryptlex.com/v3/{RELEASE_ID}?key={LICENSE_KEY}
#or
curl https://releases.cryptlex.com/v3/{RELEASE_ID}?key={LICENSE_KEY} -o="myapp.zip"

# using access token
curl -O -J -L https://releases.cryptlex.com/v3/{RELEASE_ID} \
     -H "Authorization: Bearer {ACCESS_TOKEN}"
#or
curl -O -J -L https://releases.cryptlex.com/v3/{RELEASE_ID} \
     -H "Authorization: Bearer {ACCESS_TOKEN}" \
     -o="myapp.zip"
```

The license key must belong to the product for which the release was created and access token must belong to any user who is associated with the license key of the product.

## Downloading an update

In order to detect whether an is available for your product, you need to invoke the [/v3/releases/update](https://api.cryptlex.com/v3/docs#operation/V3ReleasesUpdateGet) endpoint.

Following sample requests checks whether a new release is available by comparing with the provided release version.

{% api-method method="get" host="https://api.cryptlex.com" path="/v3/releases/update" %}
{% api-method-summary %}
Check for an update
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="productId" type="string" required=true %}
Unique identifier for the product
{% endapi-method-parameter %}

{% api-method-parameter name="platform" type="string" required=true %}
Release platform
{% endapi-method-parameter %}

{% api-method-parameter name="channel" type="string" required=false %}
Release channel \(defaults to "stable"\)
{% endapi-method-parameter %}

{% api-method-parameter name="version" type="string" required=true %}
Current release version
{% endapi-method-parameter %}

{% api-method-parameter name="key" type="string" required=true %}
License key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{ 
    "name": "MyApp v2.2", 
    "channel": "stable", 
    "version": "2.2", 
    "platform": "windows", 
    "filename": "MyApp.zip", 
    "published": true, 
    "url": "https://releases.cryptlex.com/v3/d13c8706-3dc0-42a6-89d3-6178de1c5632?key=622C02-43DFD8-4169A3-3050D8-EC8FC1-C4D894", 
    "filesize": 367660, 
    "checksum": "ef4bbff62ed6e8a24890cb438d95c445", 
    "productId": "3e8aa7eb-d175-446d-bc40-282209fd8360", 
    "notes": "Added feature X", 
    "id": "d13c8706-3dc0-42a6-89d3-6178de1c5632", 
    "createdAt": "2018-06-21T10:17:13.050285", 
    "updatedAt": "2018-06-21T10:17:46.777448" 
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

If an update is available it returns a 200 success response containing the download url, else it will return a 204 empty response.

## Downloading latest

In order to download the latest release of your product, you need to invoke the [/v3/releases/latest](https://api.cryptlex.com/v3/docs#operation/V3ReleasesLatestGet) endpoint to get the download url for the latest release.

Following sample requests fetches the latest release details.

{% api-method method="get" host="https://api.cryptlex.com" path="/v3/releases/latest" %}
{% api-method-summary %}
Download latest release
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="productId" type="string" required=true %}
Unique identifier for the product
{% endapi-method-parameter %}

{% api-method-parameter name="platform" type="string" required=true %}
Release platform
{% endapi-method-parameter %}

{% api-method-parameter name="channel" type="string" required=false %}
Release channel \(defaults to "stable"\)
{% endapi-method-parameter %}

{% api-method-parameter name="key" type="string" required=true %}
License key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{ 
    "name": "MyApp v2.2", 
    "channel": "stable", 
    "version": "2.2", 
    "platform": "windows", 
    "filename": "MyApp.zip", 
    "published": true, 
    "url": "https://releases.cryptlex.com/v3/d13c8706-3dc0-42a6-89d3-6178de1c5632?key=622C02-43DFD8-4169A3-3050D8-EC8FC1-C4D894", 
    "filesize": 367660, 
    "checksum": "ef4bbff62ed6e8a24890cb438d95c445", 
    "productId": "3e8aa7eb-d175-446d-bc40-282209fd8360", 
    "notes": "Added feature X", 
    "id": "d13c8706-3dc0-42a6-89d3-6178de1c5632", 
    "createdAt": "2018-06-21T10:17:13.050285", 
    "updatedAt": "2018-06-21T10:17:46.777448" 
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

It returns a 200 success response containing the download url of the latest release.

