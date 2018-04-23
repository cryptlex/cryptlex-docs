# Offline Activations

Suppose your user doesn't have access to an internet connection or may not have in near future. For such cases you can provide your users with an offline activation response file which can be used to activate the license offline. Offline activation process has following three steps:

## Generating offline activation request file

To allow your users to generate offline activation request file use following LexActivator API function:

```c
GenerateOfflineActivationRequest();
```

## Generating offline activation response file

Now, after getting the offline activation response file from user, go to activations page of license and click the "Offline Activation" button. You will be presented with a form, paste the contents of offline activation response file, set the validity of response and click "ACTIVATE" button. If request is valid then offline activation response file will start downloading.

## Activating using offline activation response file

To allow your users to activate using the generated offline activation response file use following LexActivator API function:

```c
ActivateLicenseOffline();
```

In case user formats the PC, the generated offline activation response can be reused, till the validity expires, to activate your app on the user's machine.

