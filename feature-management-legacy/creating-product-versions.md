# Creating Product Versions

## Using the Admin Portal

After creating a product, follow these steps to create product versions:

### 1. Create feature flags:

• Navigate to the Feature Flags page by going to `Features -> Feature Flags` in the sidebar.

• Create all necessary feature flags for your product.

### 2. Create product versions:

• Navigate to the Product Versions page by going to `Features -> Product Versions` in the sidebar.

• Create product versions for your product.

The values of each feature flag can be set when creating product versions. Any feature flags created later will automatically appear in all product versions but will be disabled by default. You can then update your product versions and set the value of each feature flag as required.

## Accessing feature flags in your application

After you have created `Product Versions` and linked it with the license, you can easily get the  product version name, product version display name and product version feature flags in your applications using the following LexActivator functions:

**`GetProductVersionName()`**

**`GetProductVersionDisplayName()`**

**`GetProductVersionFeatureFlag(string featureFlagName)`**



