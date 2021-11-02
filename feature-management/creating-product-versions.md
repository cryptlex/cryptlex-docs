# Creating Product Versions

## Using the Dashboard

After you have created a `Product`, within your Product Page, there is a button labelled Product Versions which will lead you to a page where you can create `Product Versions` for that particular `Product`. Before creating `Product Versions`, you must create `Feature Flags` by navigating via the following route:

> (Dashboard Home > Products > ProductA > Product Versions > Feature Flags)

The values of each flag can then be set when creating `Product Versions`. `Feature Flags`  created later will automatically reflect in all `Product Versions` with no data and are disabled by default. You can then update your product versions and set the value of the feature flag as required.

## Accessing feature flags in your application

After you have created `Product Versions` and linked it with the license, you can easily get the  product version name, product version display name and product version feature flags in your applications using the following LexActivator functions:

**`GetProductVersionName()`**

**`GetProductVersionDisplayName()`**

**`GetProductVersionFeatureFlag(string featureFlagName)`**



