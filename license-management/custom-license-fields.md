---
description: >-
  Using metadata properties you can store custom license data alongside
  products, licenses and users. This can include additional options to enable or
  disable specific features in your application.
---

# Custom License Fields

## Metadata properties

The metadata which can be added to products, licenses and users has following three properties:

#### Key

Name of the metadata key.

#### Value

Value of the metadata key.

#### Visible

Determines whether the metadata key/value is accessible in the app after trial or license activation.

## Product metadata

This metadata can be added to products and can be accessed in your application once a trial or license is activated.

It can be used for storing some product level information which you want to access in your app and this information can change over time.

## License metadata

This metadata can be added to your licenses at the time of creating a license. You can store additional data like `order_id`_,_ `customer_id` , `feature1`, `feature2` etc_._ with the license.

This can be accessed in your application once a license is activated. It's common use case is feature detection, i.e. if you wish to restrict the features in your application based on the value of metadata fields.

{% hint style="info" %}
In order to require licenses to have specific metadata properties, set them in license policy **requiredMetadataKeys** field**.**
{% endhint %}

## User metadata

This metadata can be added to your license users at the time of creating a user. You can store additional data like `phone_number`, `address` etc. __in the user metadata.

## Activation metadata

This metadata can be added by your application at the time of activating the license.

It can be used to collect additional details from the machine on which license is activated, e.g. number of cpu cores, any custom data provided by user etc.

## Trial activation metadata

This metadata can be added by your application at the time of activating the trial.

It can be used to collect additional details from the machine on which trial is activated, e.g. number of cpu cores, any custom data provided by user etc.

