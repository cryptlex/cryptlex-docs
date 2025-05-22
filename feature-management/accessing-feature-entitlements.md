# Accessing Feature Entitlements

Use the Cryptlex SDK, either LexActivator or LexFloatClient, to retrieve feature entitlements at runtime and apply licensing logic in your application. These entitlements determine which features should be enabled, disabled, or configured dynamically based on the active license.

You can retrieve entitlements:

* Individually, by specifying a feature name.
* As a complete list, for broader entitlement evaluation.

## Retrieve a Specific Feature Entitlement

**`GetFeatureEntitlement(string featureName)`**

This function returns the entitlement associated with the specified feature name. Internally, the resolution process follows this order:

1.  **License-Level Entitlement**

    If the feature entitlement is directly defined on the license, its value is returned.
2.  **Entitlement Set**

    If not found at the license level, the function checks whether the license is linked to an entitlement set and returns the feature entitlement from there, if present.

This allows for flexible and hierarchical entitlement management, where licenses can override defaults defined in entitlement sets when necessary.

## Retrieve All Feature Entitlements

**`GetFeatureEntitlements()`**

This function returns all feature entitlements associated with the license. Use this function when you need to evaluate multiple entitlements at once or when dynamically configuring application behavior based on the full set of features included in the license.
