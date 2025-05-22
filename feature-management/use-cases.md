# Use Cases

The following use cases demonstrate how Entitlement Sets and license-level feature entitlements in Cryptlex can be used to define product behavior, manage license tiers, and enforce custom limits.

## 1. Product Tiering

Organizations often offer multiple editions of their product, such as Standard, Pro, and Enterprise, with different capabilities. Entitlement Sets help group relevant feature entitlements into reusable tiers.

**For Example:**

| Tier       | Feature Entitlements                                                      |
| ---------- | ------------------------------------------------------------------------- |
| Standard   | `basic_export`                                                            |
| Pro        | `basic_export`, `analytics_dashboard`                                     |
| Enterprise | `basic_export`, `analytics_dashboard`, `priority_support`, `team_sharing` |

Licenses are linked to the relevant Entitlement Set, and the application logic checks which features are enabled to control access.

## 2. Usage Limits with Feature Values

Feature values can be used to define usage limits, such as the number of projects, users, or API calls.

**Example:**

* Feature: `max_team_members`
* Value: `5`, `20`, or `unlimited`
* Usage: The application reads the value at runtime and enforces the limit accordingly.

This approach enables dynamic limits without requiring new builds or manual configuration.

## 3. Controlled Feature Rollouts (Beta Access)

Entitlements can be used to enable or disable features for a specific group of users, such as beta testers.

**Example:**

* Features: `beta_dark_mode`, `ai_autocomplete`
* Added only to selected licenses
* Application checks for feature presence before enabling UI or functionality

This allows safe, controlled rollouts without the need for separate builds.
