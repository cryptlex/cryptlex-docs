# Offline Activations

Suppose your user doesn't have access to an internet connection or may not have it in the near future. For such cases, you can provide your users with an offline activation response file which can be used to activate the license offline. The offline activation process has the following three steps:

## Generating offline activation request file

To allow your users to generate offline activation request files, after setting the license key, use the following LexActivator API function:

```c
SetLicenseKey("PASTE_LICENCE_KEY");
GenerateOfflineActivationRequest();
```

{% hint style="info" %}
The `GenerateOfflineActivationRequest()` function requires a valid file path (including the complete file name and extension).
{% endhint %}

## Generating offline activation response file

Now, after getting the offline activation request file from the user, go to `Activations` page in the admin portal and  click the **`CREATE OFFLINE`** button. You will be presented with a form, upload the offline activation request file, set the validity for the response file and click **`ACTIVATE`** button. If the request is valid then the offline activation response file will start downloading.

{% hint style="info" %}
Your customers can also log into the customer portal, to download the offline activation response file by themselves, saving you a considerable amount of time on product support.
{% endhint %}

## Activating using offline activation response file

To allow your users to activate using the generated offline activation response file use the following LexActivator API function:

```c
ActivateLicenseOffline();
```

{% hint style="info" %}
The `ActivateLicenseOffline()` function requires a valid file path (including the file name and extension).
{% endhint %}

In case the user formats the PC, the generated offline activation response can be reused to activate your app, till the response validity expires.
