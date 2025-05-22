# License Feature Entitlements

Feature entitlements define what a license enables within your product. In Cryptlex, features can be associated with a license in two ways: via Entitlement Sets or directly on the license itself. This flexibility allows both standardized tier-based licensing and custom per-customer overrides.

## Linking Feature Entitlements via Entitlement Sets

Entitlement Sets serve as reusable bundles of feature entitlements that can be linked to multiple licenses.

**Use When**:

* You offer predefined product tiers like "Standard", "Pro", or "Enterprise"
* You want to ensure consistency across licenses
* You prefer centralized management of feature entitlements

## Assigning Features Entitlements Directly to a License

Feature entitlements can also be added directly to a license without using an Entitlement Set.

**Use When**:

* Each customer requires a specific configuration outside the standard tiers
* You need to override a value from the Entitlement Set for a specific license
* You want to grant temporary or experimental access to a feature

## Combining Both Approaches

Cryptlex supports a hybrid approach where a license can use both an Entitlement Set and additional direct license-level feature entitlements.

**Example**:

* License uses the `Pro` Entitlement Set (with feature entitlement `max_projects = 20`)
* You override `max_projects = 50` directly on the license
* You also add `priority_support` directly for this specific customer
