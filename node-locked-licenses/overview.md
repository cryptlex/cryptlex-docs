# Overview

## Node locked licenses

The basic concept of node-locked licensing is that your application should contact an online license server, to confirm the validity of the license key provided by the user to activate the license.&#x20;

At the time of license activation, it should also generate a unique device fingerprint, and send it along with the license activation request.&#x20;

The license server must store the device fingerprint and use it to validate the license key for further activations to prevent the usage of the license key on other devices.

## What is LexActivator

LexActivator is basically a **libcurl** based HTTP client which invokes Cryptlex Web API endpoints from your application to activate your licenses and trials.

These licensing API endpoints can be invoked using any HTTP library, but it does something more which can save you a lot of time:

* Abstracts away HTTPS part, so you basically call simple functions like `ActivateLicense(),` `ActivateTrial()` etc. instead of sending HTTPS requests.
* Verifies the HTTPS response signature using **2048 bit RSA** public key.
* Stores the HTTPS response in an encrypted form on the disk using **AES 128 bit** symmetric encryption algorithm.
* Generates multiple fingerprints of the machine using an **advanced device fingerprinting algorithm**, which can be used to allow for different fingerprint matching strategies.
* Does virtual machine detection so you can prevent users from activating your licenses in virtual machines. Virtual machines can be cloned which may sometimes result in the same fingerprint on different machines.
* Periodically invokes the Cryptlex API endpoints in a separate thread to sync the server license data with the client.
* Handles the offline activations.

## Minimum requirements

* **Windows**: Supported from Windows 7 and above.
* **macOS**: Supported from macOS 10.13 and above.
* **Linux**: Compatible with all major distributions with a minimum required **glibc version of 2.13**.
* **Android**: Minimum supported **API level 23** and **NDK version r21e**.
* **iOS**: Supported on devices running **iOS 11.0 and later**.

LexActivator supports both **32-bit and 64-bit architectures** on all desktop platforms. In addition, **ARM architecture** is supported on **Windows**, **macOS** and **Linux**.
