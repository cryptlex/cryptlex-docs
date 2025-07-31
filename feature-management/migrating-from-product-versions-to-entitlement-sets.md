# Migrating from Product Versions to Entitlement Sets

This guide outlines a clear, step-by-step process to help you transition seamlessly from the legacy **Product Versions** model to the new Entitlement Sets. It is designed to ensure a smooth migration with minimal disruption to your current setup.

## **Step-by-Step Migration Guide:**

#### **1. Define Features and Entitlement Sets**

* Log in to the Cryptlex Admin portal.
* Navigate to [**Entitlements > Features**](https://app.cryptlex.com/entitlements/features).
* Create the features you want to control access to, similar to the existing feature flags.
* Go to [**Entitlements > Entitlement Sets**](https://app.cryptlex.com/entitlements/entitlement-sets).
* Create new entitlement sets, the same as the existing product versions, and add the relevant features.

### **2. Update License Configuration**

* Assign the entitlement set to the appropriate licenses.
* You can also assign feature entitlements directly to a license if needed.

### **3. Upgrade the SDK version**

* Ensure you are using [LexActivator](https://app.cryptlex.com/developer/sdk-downloads) v3.32.3 or above.
* Update your integration to use `GetFeatureEntitlement()` instead of `GetProductVersionFeatureFlag()`.

### **4. Modify Application Logic**

* Replace any product version checks with feature entitlement checks. For example:

| Legacy Concept                   | New Equivalent                                                                                                                 |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Product Version**              | **Entitlement Set**                                                                                                            |
| **Feature Flag**                 | **Feature Entitlement**                                                                                                        |
| `GetProductVersionFeatureFlag()` | [`GetFeatureEntitlement()`](https://github.com/cryptlex/lexactivator-c/blob/master/examples/LexActivator.h#L608)               |
| `GetProductVersionName()`        | [`GetLicenseEntitlementSetName()`](https://github.com/cryptlex/lexactivator-c/blob/master/examples/LexActivator.h#L558)        |
| `GetProductVersionDisplayName()` | [`GetLicenseEntitlementSetDisplayName()`](https://github.com/cryptlex/lexactivator-c/blob/master/examples/LexActivator.h#L572) |

### **5. Gradual Rollout**

* Continue using the legacy system for older versions of your application.
* Start using the Entitlements system in newer application versions.
* Once all active users are on the newer version, deprecate and remove legacy checks.

## **Need Assistance?**

Our [support](mailto:support@cryptlex.com) team is here to assist you throughout the transition. Feel free to reach out if you need any help.
