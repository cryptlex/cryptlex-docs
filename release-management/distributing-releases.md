# Distributing Releases

## Downloading a release

In order to download the release, the release URL must contain license key as  **`key`** query parameter or **`access token`** in the header.

```bash
# download file using license key
curl https://releases.cryptlex.com/v3/{ACCOUNT_ID}/{RELEASE_ID}/myapp.zip?key={LICENSE_KEY} \
     -o="myapp.zip"

# download file using access token
curl -O -J -L https://releases.cryptlex.com/v3/{ACCOUNT_ID}/{RELEASE_ID}/myapp.zip \
     -H "Authorization: Bearer {ACCESS_TOKEN}" \
     -o="myapp.zip"
```

The license key must belong to the product for which the release was created and the access token must belong to any user who is associated with the license key of the product.

{% hint style="danger" %}
The external release files are not secured and hence don't require**`key`** query parameter for download.
{% endhint %}

## Downloading an update

In order to detect whether an update is available for your product, you can either invoke the [/v3/releases/update](https://api.cryptlex.com/v3/docs#operation/get/v3/releases/update) Web API endpoint or use **`CheckReleaseUpdate()`** LexActivator function.

### Using Web API

The following sample request checks whether a new release is available by comparing it with the provided release version.

{% swagger baseUrl="https://api.cryptlex.com" path="/v3/releases/update" method="get" summary="Check for an update" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="accountId" required="true" type="string" %}
Unique identifier for the account
{% endswagger-parameter %}

{% swagger-parameter in="query" name="productId" type="string" required="true" %}
Unique identifier for the product
{% endswagger-parameter %}

{% swagger-parameter in="query" name="platform" type="string" required="true" %}
Release platform
{% endswagger-parameter %}

{% swagger-parameter in="query" name="channel" type="string" required="false" %}
Release channel (defaults to "stable")
{% endswagger-parameter %}

{% swagger-parameter in="query" name="version" type="string" required="true" %}
Current release version
{% endswagger-parameter %}

{% swagger-parameter in="query" name="key" type="string" required="true" %}
License key
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```javascript
{
  "name": "MyApp v2.2",
  "channel": "stable",
  "version": "2.3",
  "platform": "windows",
  "published": true,
  "productId": "3e7aa7eb-d175-446d-bc40-282209fd8360",
  "notes": "Added feature X",
  "files": [
    {
      "name": "myapp.exe",
      "url": "https://releases.cryptlex.com/v3/155f79fc-2f28-40b2-afc5-3fcc6c63225a/myapp.exe",
      "size": 37580,
      "checksum": "1239d72ef6ff110ef63a803120728907",
      "releaseId": "155f79fc-2f28-40b2-afc5-3fcc6c63225a",
      "id": "7ca34eed-05be-4799-8b3d-f00d5440c5da",
      "createdAt": "2018-06-29T13:11:33.852642",
      "updatedAt": "2018-06-29T13:11:33.852643"
    },
    {
      "name": "myapp.zip",
      "url": "https://releases.cryptlex.com/v3/155f79fc-2f28-40b2-afc5-3fcc6c63225a/myapp.zip",
      "size": 5510,
      "checksum": "8892af7769c1147f9801c1a5aab52cce",
      "releaseId": "155f79fc-2f28-40b2-afc5-3fcc6c63225a",
      "id": "685eaa15-33bc-4443-89e4-baf733a6c34d",
      "createdAt": "2018-06-29T13:08:59.175004",
      "updatedAt": "2018-06-29T13:11:33.563872"
    }
  ],
  "id": "155f79fc-2f28-40b2-afc5-3fcc6c63225a",
  "createdAt": "2018-06-29T08:55:03.515291",
  "updatedAt": "2018-06-29T08:55:03.515414"
}
```
{% endswagger-response %}
{% endswagger %}

If an update is available it returns a **`200`** success response containing the download URL, else it will return a **`204`** empty response.

### Using LexActivator

The sample code for checking the release update is available on GitHub for all the languages in their sample files. The following sample code demonstrates it for C/C++.

```cpp
void LA_CC SoftwareReleaseUpdateCallback(int status, Release* release, void* custom_data)
{
	switch (status)
	{
	case LA_RELEASE_UPDATE_AVAILABLE:
		printf("A new update is available for the app.\n");
		printf("Release notes: %s", release->notes);
		break;

	case LA_RELEASE_UPDATE_AVAILABLE_NOT_ALLOWED:
		printf("A new update is available for the app but it's not allowed.\n");
		printf("Release notes: %s", release->notes);
		break;

	case LA_RELEASE_UPDATE_NOT_AVAILABLE:
		printf("Current version is already latest.\n");
		break;

	default:
		printf("Error code: %d\n", status);
	}
}

int main()
{
	int status;
	// init code - SetProductId(), SetProductData()
	// ...
	status = SetReleasePlatform("windows");
	if (LA_OK != status)
	{
		// handle error
	}
	status = SetReleaseChannel("stable");
	if (LA_OK != status)
	{
		// handle error
	}
	status = SetReleaseVersion("1.2.3.4");
	if (LA_OK != status)
	{
		// handle error
	}
	status = CheckReleaseUpdate(SoftwareReleaseUpdateCallback, LA_RELEASES_ALL, data);
	if (LA_OK != status)
	{
		printf("Error checking for software release update: %d", status);
	}
}

```

### Ignoring PATCH and BUILD updates

The version format syntax in Cryptlex is **`$MAJOR.$MINOR.$PATCH.$BUILD`.** In case you want to ignore **`$PATCH`** and **`$BUILD`** releases in the update API endpoint you can pass the partial version too.&#x20;

The following table summarises the expected response by the `/v3/releases/update` API endpoint if it is invoked with **`version`** query param set to the values in the first column:

| Version (Query Param) | Latest Version | Response (Status Code) |
| --------------------- | -------------- | ---------------------- |
| 1.2.3.5               | 1.2.3.5        | 204                    |
| 1.2.3.4               | 1.2.3.5        | 200                    |
| 1.2.3                 | 1.2.3.4        | 204                    |
| 1.2                   | 1.2.3.4        | 204                    |

Suppose your latest release version is **`1.2.3.4`** and you invoke the update API endpoint with **`version`** query param having a value **`1.2.3`**, then it will return **`204`** status code indicating no update.

## Downloading latest

In order to download the latest release of your product, you need to invoke the [/v3/releases/latest](https://api.cryptlex.com/v3/docs#operation/get/v3/releases/latest) endpoint to get the download URLs for the latest release.

The following sample request fetches the latest release details.

{% swagger baseUrl="https://api.cryptlex.com" path="/v3/releases/latest" method="get" summary="Download latest release" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="accountId" type="string" %}
Unique identifier for the account
{% endswagger-parameter %}

{% swagger-parameter in="query" name="productId" type="string" required="true" %}
Unique identifier for the product
{% endswagger-parameter %}

{% swagger-parameter in="query" name="platform" type="string" required="true" %}
Release platform
{% endswagger-parameter %}

{% swagger-parameter in="query" name="channel" type="string" required="false" %}
Release channel (defaults to "stable")
{% endswagger-parameter %}

{% swagger-parameter in="query" name="key" type="string" required="true" %}
License key
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```javascript
{
  "name": "MyApp v2.2",
  "channel": "stable",
  "version": "2.3",
  "platform": "windows",
  "published": true,
  "productId": "3e7aa7eb-d175-446d-bc40-282209fd8360",
  "notes": "Added feature X",
  "files": [
    {
      "name": "myapp.exe",
      "url": "https://releases.cryptlex.com/v3/155f79fc-2f28-40b2-afc5-3fcc6c63225a/myapp.exe",
      "size": 37580,
      "checksum": "1239d72ef6ff110ef63a803120728907",
      "releaseId": "155f79fc-2f28-40b2-afc5-3fcc6c63225a",
      "id": "7ca34eed-05be-4799-8b3d-f00d5440c5da",
      "createdAt": "2018-06-29T13:11:33.852642",
      "updatedAt": "2018-06-29T13:11:33.852643"
    },
    {
      "name": "myapp.zip",
      "url": "https://releases.cryptlex.com/v3/155f79fc-2f28-40b2-afc5-3fcc6c63225a/myapp.zip",
      "size": 5510,
      "checksum": "8892af7769c1147f9801c1a5aab52cce",
      "releaseId": "155f79fc-2f28-40b2-afc5-3fcc6c63225a",
      "id": "685eaa15-33bc-4443-89e4-baf733a6c34d",
      "createdAt": "2018-06-29T13:08:59.175004",
      "updatedAt": "2018-06-29T13:11:33.563872"
    }
  ],
  "id": "155f79fc-2f28-40b2-afc5-3fcc6c63225a",
  "createdAt": "2018-06-29T08:55:03.515291",
  "updatedAt": "2018-06-29T08:55:03.515414"
}
```
{% endswagger-response %}
{% endswagger %}

It returns a **`200`** success response containing the download URLs of the latest release.
