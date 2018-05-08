---
description: Let's quickly go through the terminology we use in Cryptlex.
---

# Overview

## Product

A product refers to your application which you want to license. 

You can create a single product for all your application versions or you can create multiple products for your different application versions. e.g. if you offer two versions of your app PRO and LITE then you can choose to create two products.

## License policy

A license policy helps you create different types of license profiles. It acts as a blueprint for the licenses you create for your customers and helps you implement different types of licensing models.

A single license policy can be shared across different products and each product must have a license policy.

## Trial policy

A trial policy is similar to a license policy, with the difference that it is applicable for trials only. You can create a trial policy using license policies too, but this offers you a cheap and convenient way of doing so.

A single trial policy can be shared across different products and each product may have a trial policy. Not attaching a trial policy to a product disables trials automatically.

## User

A user refers to your customer whom you want to license your product. 

Cryptlex provides identity management for your customers, which means you can authenticate your customers using email/password, and other features like password reset etc.

## License

A license is what you use to license your application. Licenses are grouped under products and inherit all the properties of license policy attached to the product.

You can override all the properties of the license inherited from a license policy if needed.

{% hint style="info" %}
You may or may not attach a user to a license depending on whether you want store your user data in Cryptlex or not.
{% endhint %}

## Activation

A license activation is said to occur when your customer uses a license key to activate the license in your application on his/her machine.

By default all activations are node-locked, it means that the machine fingerprint is stored along with the activation details.

## Trial activation

A trial activation is said to occur when your customer activates the trial in your application on his/her machine.

By default all trial activations are node-locked, it means that the machine fingerprint is stored along with the trial activation details.

