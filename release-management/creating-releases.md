# Creating Releases

Whenever you release a new version of your software, you will need to create a new release in the Cryptlex admin portal (or through Web API). After you create the release, you have to upload your software bundle with the release. You can also host the software bundle on your server.

## Creating a release

You can easily create a release through the admin portal. Go to the Releases section in the sidebar and click the **`Add`** button. A create release form with the following fields will popup:&#x20;

#### Name

The name of the release. This can be a user-friendly name to identify the release e.g. MyApp v1.2.

#### Version

The version format syntax in Cryptlex is **`$MAJOR.$MINOR.$PATCH.$BUILD`.** So, only the following three formats are allowed:

* x.x - **`$MAJOR.$MINOR`**
* x.x.x - **`$MAJOR.$MINOR.$PATCH`**
* x.x.x.x - **`$MAJOR.$MINOR.$PATCH.$BUILD`**

&#x20;It must only contain dot-separated digits e.g. 1.2, 1.2.3, 1.2.3.4, etc.

#### Platforms

The platforms of the release. It will usually have any of the following values: windows, linux, macos, win32, win64, etc.

#### Channel

The channel of the release. The default value is **stable**. You can use it to differentiate between alpha, beta, RC, stable, etc. release types.

#### Notes

The release notes for the release. It also supports [markdown](https://www.markdownguide.org/basic-syntax).

## Uploading release file

In the create release form you need to upload the release files too which need to be distributed securely to your licensed users.

The release file can also be uploaded using any command-line HTTP client like **curl**. To upload the release file using **curl** execute the following command:

```bash
curl -X PUT https://releases.cryptlex.com/v3/{RELEASE_ID}/myapp.zip \
     -H "Authorization: Bearer {ACCESS_TOKEN}" \
     -T "/path/to/myapp.zip"

# In case you are using Cryptlex On-Premise then use following instead
curl -X PUT https://releases.mycompany.com/v3/{RELEASE_ID}/myapp.zip \
     -H "Authorization: Bearer {ACCESS_TOKEN}" \
     -F "file=@/path/to/myapp.zip"
```

The access token must have at least the following two permissions: `release:read`, `release:write`.

{% hint style="danger" %}
The file name in the upload URL must only contain letters, numbers and some special characters, including. (period), - (hyphen) and \_ (underscore).
{% endhint %}

## Adding an external release file

Instead of uploading release files to our server, you can also add the release files hosted on your server.

To add the external release files click the **`Add External File`** option in the actions menu. Put in the details of your external release file in the form and click the **`Add File`** button. After that, you can see the entry in the **`Files`** column of the table.

## Publishing release

Once all the changes have been finalized you can click the **`Publish`** button to freeze the release. After a release is published it becomes read-only.
