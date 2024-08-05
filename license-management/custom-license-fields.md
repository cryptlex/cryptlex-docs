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

It can be used for storing some product-level information that you want to access in your app and this information can change over time.

## License metadata

This metadata can be added to your licenses at the time of creating a license. You can store additional data like `order_id`_,_ `customer_id` , `feature1`, `feature2` etc_._ with the license.

This can be accessed in your application once a license is activated. Its common use case is feature detection, i.e. if you wish to restrict the features in your application based on the value of metadata fields.

{% hint style="info" %}
In order to require licenses to have specific metadata properties, set them in the license template **requiredMetadataKeys** field**.**
{% endhint %}

### Enforcing schema for metadata fields

You can enforce the schema for metadata fields in the license template too, so you don't have to manually create the fields every time you create a license. Just provide the field names as comma-separated strings e.g. `order_id`_,_ `customer_id` , `feature1`, `feature2` etc. in the required metadata keys property of the license template.

## User metadata

This metadata can be added to your license users at the time of creating a user. You can store additional data like `phone_number`, `address` etc. in the user metadata.

## Activation metadata

This metadata can be added by your application at the time of activating the license.

It can be used to collect additional details from the machine on which the license is activated, e.g. number of CPU cores, any custom data provided by the user etc.

## Trial activation metadata

This metadata can be added by your application at the time of activating the trial.

It can be used to collect additional details from the machine on which the trial is activated, e.g. number of CPU cores, any custom data provided by the user etc.
