# Overview

## Node locked licenses

The basic concept of node locked licensing is that your application should contact an online license server, to confirm the validity of the license key provided by the user to activate the license. 

At the time of license activation it should also generate a unique device fingerprint, and send it along with the license activation request. 

The license server must store the device fingerprint and use it to validate the license key for further activations to prevent the usage of license key on other devices.

## What is LexActivator

LexActivator is basically a **libcurl** based HTTP client which invokes Cryptlex Web API endpoints from your application to activate your licenses and trials.

These licensing API endpoints can be invoked using using any HTTP library, but it does something more which can save you a lot of time:

* Abstracts away HTTPS part, so you basically call simple functions like `ActivateLicense(),` `ActivateTrial()` etc. instead of sending HTTPS requests.
* Verifies the HTTPS response signature using **2048 bit RSA** public key.
* Stores the HTTPS response in an encrypted form on the disk using **AES 128 bit** symmetric encryption algorithm.
* Generates multiple fingerprints of the machine, which can be used to allow for different fingerprint matching strategies.
* Does virtual machine detection so you can prevent users from activating your license in virtual machines. Virtual machines can be cloned which may sometimes result in same fingerprint on different machines.
* Periodically invokes the Cryptlex API endpoints in a separate thread to sync the server license data with the client.
* Handles the offline activations.

## Minimum requirements

LexActivator works on Windows XP through Windows 10, MacOS 10.6+ and all Linux distributions \(minimum supported `glibc` library version is `v2.13` and `libnss3` library version is `v3.12`\).

There are no additional dependencies. It supports 32 bit as well as 64 bit cpu architectures for all the platforms. Additionally, for Linux ARM cpu architecture is also supported.

