# Licensing Docker Apps

## Licensing Docker apps

When an app runs inside a Docker, it gives very little access to the host hardware details. Hence it is difficult to generate a quality device fingerprint.

This makes node-locked licensing almost useless in case of apps running inside Docker. And if you decide to use node-locked licenses, then your customers can easily use the same license key across different Docker instances running on the same or different devices.

## Using floating licenses

[Floating licenses](floating-licenses/) are the best way to license Docker applications. For apps having access to the internet, you should use hosted-floating license type and apps which have no access to the internet you should use on-premise floating license type.&#x20;

Also, ensure [leasing strategy](https://docs.cryptlex.com/license-management/license-templates#leasing-strategy) for the license is set to **"per-instance".**

When you set the leasing strategy to **"per-instance"**, it ensures a new license activation is consumed whenever your app sends an activation request irrespective of whether the device fingerprint is the same or different.

