# Overview

## Product

A product refers to the application you want to license.

You should create a single product for your application, regardless of its different versions (e.g., Lite, Pro, Business, Ultimate, etc). However, for different applications, separate products should be created.

## License template

A license template helps you create different types of license profiles/configurations. It acts as a blueprint for the licenses you create for your customers and helps you implement different types of licensing models.

A single license template can be shared across different products and each product must have a default license template linked.

## Trial policy

A trial policy allows you to configure trials for your product.

A single trial policy can be shared across different products and each product may have a trial policy. Not attaching a trial policy to a product disables trials automatically.

## User

A user refers to your customer whom you want to license your product.&#x20;

Cryptlex provides identity management for your customers, which means you can authenticate your customers using email/password, and other features like password reset etc.

## License

A license is what you use to license your application. Licenses are grouped under products and inherit all the properties of license template attached to the product.

You can override all the properties of the license inherited from a license template if needed.

{% hint style="info" %}
You may or may not attach a user to a license depending on whether you want store your user data in Cryptlex or not.
{% endhint %}

## Activation

A license activation is said to occur when your customer uses a license key to activate the license in your application on his/her machine.

By default, all activations are node-locked, which means that the machine fingerprint is stored along with the activation details.

## Trial activation

A trial activation is said to occur when your customer activates the trial in your application on their machine.

By default, all trial activations are node-locked, which means that the machine fingerprint is stored along with the trial activation details.

## Release

A release helps you manage different release versions of your app and allows you to host your app on our servers for secure distribution. It also allows you to deliver software updates.

## Cryptlex Web API

Cryptlex web API lets you implement any software licensing model with node-locked licensing, floating licensing, perpetual licenses, subscriptions, timed trials and more supported out of the box.&#x20;

It also provides identity management for your customers, which means you can authenticate your customers using email and password, and provide other features like profile management.

## LexActivator - Cryptlex Licensing Library

LexActivator makes it dead simple to implement any type of licensing model, including hosted floating licenses, by abstracting away HTTPS network requests, AES encryption, RSA signature verification, advanced machine fingerprinting, virtual machine detection and much more.

## LexFloatServer & LexFloatClient

An on-premise floating license server to help you implement a floating licensing model inside networks which may or may not be connected to the internet.
