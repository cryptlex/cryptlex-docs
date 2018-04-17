# Offline Activation

Suppose your user doesn't have access to an internet connection or may not have in near future. For such cases you can provide your users with an offline activation response file which can be used to activate the product offline. Offline activation process has following three steps:

## Generating offline activation request file

To allow your users to generate offline activation request file use following LexActivator API function:

```text
GenerateOfflineActivationRequest();
```

## Generating offline activation response file

Now, after getting the offline activation response file from user, go to product version page and click the "Offline Activation" button. You will be presented with a form, paste the contents of offline activation response file, set the validity of response and click "Validate Request" button. If request is valid you will be prompted to download the offline activation response file.

![offline-activation](https://cryptlex.com/public/img/docs/offline-activation.png)

## Activating using offline activation response file

To allow your users to activate using the generated offline activation response file use following LexActivator API function:

```text
ActivateProductOffline();
```

In case user formats the PC, the generated offline activation response can be reused, till the validity expires, to activate your app on the user's machine.

