---
description: >-
  LexActivator is the library which you include in your app to invoke Cryptlex
  Web API. It adds support for license activations, license offline activations,
  and trials in your app.
---

# Using LexActivator

## Why use LexActivator

LexActivator is basically a **libcurl** based HTTP client which invokes Cryptlex Web API endpoints from your application to activate your licenses and trials.

You can do this yourself too in your app using any HTTP library, but it does something more which can save you a lot of time:

* Abstracts away HTTP part, so you basically call simple functions like `ActivateLicense(),` `ActivateTrial()` etc. instead of sending HTTP requests.
* Verifies the HTTP response signature using RSA public key.
* Stores the HTTP response in an encrypted form on the disk.
* Generates multiple fingerprints of the machine, which can be used to allow for different fingerprint matching strategies.
* Does virtual machine detection so you can prevent users from activating your license in virtual machines. Virtual machines can be cloned which may sometimes result in same fingerprint on different machines.
* Periodically invokes the Cryptlex API endpoints in a separate thread to sync the server license data with the client.
* Handles the offline activations.

If you think you want do it yourself then you can skip this tutorial and move on.

## Integrating LexActivator in your App

You can use any** programming language** to integrate LexActivator with any app that runs on Windows, MacOS or Linux. Following are tutorials for some commonly used programming languages:

* [Using LexActivator with C, C++, and Objective-C](https://cryptlex.com/help/using-lexactivator/with-c)
* [Using LexActivator with C\#](https://cryptlex.com/help/using-lexactivator/with-c-sharp)
* [Using LexActivator with Delphi](https://cryptlex.com/help/using-lexactivator/with-delphi)
* [Using LexActivator with Java](https://cryptlex.com/help/using-lexactivator/with-java)
* [Using LexActivator with VB.NET](https://cryptlex.com/help/using-lexactivator/with-vb-net)

## Minimum Requirements

LexActivator works on Windows XP through Windows 10, MacOS 10.6+ and all Linux distributions \(minimum supported glibc library version is 2.13\).

There are no additional dependencies. It supports 32 bit as well as 64 bit cpu architectures for all the platforms. Additionally, for Linux ARM cpu architecture is also supported.
