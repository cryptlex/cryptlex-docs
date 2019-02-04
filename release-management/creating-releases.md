# Creating Releases

## Creating a release

You can easily create a release through dashboard. Go to the releases option in the dashboard under products section and click the add the button. A release form with following fields will popup: 

#### Name

The name of the release. This can be a user friendly name to identify the release e.g. MyApp v1.2.

#### Version

The version of the release. Only following three formats are allowed `x.x`, `x.x.x`, `x.x.x.x`. It must only contain dot separated digits e.g. 1.2, 1.2.3, 1.2.3.4 etc.

#### Platform

The platform of the release. It will usually have one of the following values: windows, linux, macos, win32, win64 etc.

#### Channel

The channel of the release. The default value is **stable**. You can use it to differentiate between alpha, beta, rc, stable etc. release types.

#### Notes

The release notes for the release. It also supports [markdown](https://www.markdownguide.org/basic-syntax).

## Uploading release file

After the release is created you need to upload the release file which needs to be distributed securely to your licensed users.

In order to upload the file select the release in the dashboard and click the "**Upload Files**" button. After the successful upload you can see the the entry in the "**Files**" section at the bottom.

The release can also be uploaded using any command line HTTP client like **curl**. To upload the release file using **curl** execute the following command:

```bash
curl -X PUT https://releases.cryptlex.com/v3/{RELEASE_ID}/myapp.zip \
     -H "Authorization: Bearer {ACCESS_TOKEN}" \
     -F "file=@/path/to/myapp.zip"
```

The access token must have at least following two permissions: `release:read`, `release:write`.

{% hint style="danger" %}
The file name in the upload URL must only contain letters, numbers and some special characters, including  . \(period\), - \(hyphen\) and \_ \(underscore\).
{% endhint %}

## Publishing release

Once all the changes have been finalized you can click the "**Publish**" button to freeze the release. After a release is published it becomes readonly.

