# Maintenance Policies

A maintenance policy can be used to configure how the end-user can update the software (product). You can add restrictions on the major version, minor version and duration of updates.

A maintenance policy can be used to configure how the end-user can update the software (product). You can add restrictions on the major version, minor version and duration for which the updates will be available. The maintenance policy once created can be linked to the licenses.

{% hint style="info" %}
**NOTE:** Maintenance policies do not require using our [Release Management](../release-management/) service.
{% endhint %}

## Maintenance policy properties

The maintenance policy has the following properties:

### Name

Name of the maintenance policy.

### Validity

The duration (in seconds) after which the maintenance for the software updates of a license will expire. For unlimited duration set the validity to zero.

### Expiration Strategy

The expiration strategy determines the expiration start date of the maintenance. It allows for the following strategies:

#### **Immediate:**&#x20;

The license maintenance starts expiring right after it is created.

#### **Delayed:**&#x20;

The license maintenance starts expiring after the license is activated the first time.

### Allow Major Version Updates

If set to true then all the major version updates will be allowed till the license maintenance expires.

### Allow Minor Version Updates

If set to true then all the minor version updates will be allowed till the license maintenance expires.

## Using maintenance policies

After you have created a maintenance policy and linked it with the license, you need to call the following LexActivator function in your code after calling `SetProductId()` function:&#x20;

**`SetReleaseVersion("1.2.3");`**

The allowed version format syntax is **`$MAJOR.$MINOR.$PATCH.$BUILD`.** So, only following three formats are allowed:

* x.x - **`$MAJOR.$MINOR`**
* x.x.x - **`$MAJOR.$MINOR.$PATCH`**
* x.x.x.x - **`$MAJOR.$MINOR.$PATCH.$BUILD`**

&#x20;It must only contain dot-separated digits e.g. 1.2, 1.2.3, 1.2.3.4, etc.

The version set in this function is stored in the license as `"CurrentReleaseVersion"` property and in the activation as `"ReleaseVersion"` property. If the license has more than one activation the `"CurrentReleaseVersion"` property of the license will store the max release version.

## Using max allowed release version

In case your use-case is simple and you want to allow updates up to a particular max version, then you don't need to create any maintenance policy. Just set the `"MaxAllowedReleaseVersion"` property of the license to the max version up to which you want to allow updates. And in your application just call **`SetReleaseVersion("x.x.x")`** function.

## Renewing maintenance

Whenever you create a license and link a maintenance policy with validity say 365 days, you will see a property in the license resource named `maintenanceExpiresAt`. It is a read-only, computed property and determines the time when the license maintenance will expire.

If the license maintenance policy expiration strategy is set to `immediate`, the `maintenanceExpiresAt` property will be populated with the date on which the license maintenance will expire starting from the time when the license was created.

If the license maintenance policy expiration strategy is set to `delayed`, the `maintenanceExpiresAt` property will be `null` till the license is activated, as the license maintenance will start expiring after it is used.

To renew the license maintenance you need to invoke the [license maintenance renew endpoint](https://api.cryptlex.com/v3/docs#tag/Licenses/operation/post/v3/licenses/%7Bid%7D/maintenance/renew) or renew it through the license page on the Dashboard. It extends the license maintenance expiry by its maintenance policy's validity.

## Possible use cases

### 1- Lifetime free updates

Don’t create any policy or create the policy with the following values:

| Validity                 | 0    |
| ------------------------ | ---- |
| AllowMajorVersionUpdates | true |
| AllowMinorVersionUpdates | true |

### 2- Lifetime minor version updates

| Validity                 | 0     |
| ------------------------ | ----- |
| AllowMajorVersionUpdates | false |
| AllowMinorVersionUpdates | true  |

### 3- One-year major version updates

| Validity                 | 365 Days |
| ------------------------ | -------- |
| AllowMajorVersionUpdates | true     |
| AllowMinorVersionUpdates | true     |

### 4- One-year minor version updates

| Validity                 | 365 Days |
| ------------------------ | -------- |
| AllowMajorVersionUpdates | false    |
| AllowMinorVersionUpdates | true     |

### 5- No updates

| Validity                 | 0 (or any value) |
| ------------------------ | ---------------- |
| AllowMajorVersionUpdates | false            |
| AllowMinorVersionUpdates | false            |

