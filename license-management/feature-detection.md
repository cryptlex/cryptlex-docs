# Feature Detection

## Implementing feature detection

Your app may have many features like **Feature A**, **Feature B, Feature C** and a customer may only pay for Feature A and Feature B. So you need to prevent your customer from using Feature C.

To implement this, simply create [license metadata](https://docs.cryptlex.com/license-management/custom-license-fields) fields **feature\_a**, **feature\_b**, **feature\_c** and set a **truthy** \(yes/ true\) or **falsy** \(no/false\) value for the same at the time of license creation.

You can then access these metadata fields in your app to allow or disallow the features accordingly. Their values can be updated later on when your customer pays for that feature.

### Enforcing schema for metadata fields

You can enforce the schema for metadata fields in the license policy too, so you don't have to manually create the fields every time you create a license. Just provide the field names as comma separated strings e.g. **feature1**, **feature2**, **feature3** etc. in the [required metadata keys](https://docs.cryptlex.com/license-management/license-policies#required-metadata-keys) property of the license policy.

