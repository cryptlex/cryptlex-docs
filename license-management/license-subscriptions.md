# License Subscriptions

## Subscriptions

In Cryptlex, a subscription is a time-based licensing model where a license is valid for a specific duration (e.g., months or years). It offers flexible access control, making it ideal for recurring billing and time-limited access. A subscription can be configured by setting a subscription interval or specifying an exact expiration date.

### Adding a Subscription to a License

To configure a subscription in a license, you can define:

* A **subscription interval** and **start trigger**, or
* A fixed **expiration date**

These settings define the start of the license term and how its expiry is determined.

### 1. Using Subscription Interval and Start Trigger

To define a recurring subscription, use the `subscriptionInterval` property to specify the duration and the `subscriptionStartTrigger` to determine when that duration begins.

* Subscription Interval accepts intervals using ISO8601 durations (`P1Y`, `P3M10D`, `P30D`). This automatically accounts for varying lengths of months and years.
* Subscription Start Trigger controls when the subscription period begins:
  * **License Creation**: The subscription starts when the license is created, useful for aligning with the purchase date.
  * **License Activation**: The subscription starts when the license is first activated, useful if it should begin with the first product use.

### 2. Using Expiration Date

Alternatively, you can set a fixed expiration date by setting the `expiresAt` property of the license to define exactly when the license should expire.

## Renewing a Subscription

When a subscription is renewed, Cryptlex adds the current `subscriptionInterval` to the expiration date, renewing the license for another cycle. The license can be renewed from the admin portal manually or by using our REST API.

* **Admin Portal:** Go to the [Licenses](https://app.cryptlex.com/license-management/licenses) page, click the Actions menu (three dots) next to the license, and select **Renew License**.
* **Web API:** Send a `POST` request to the [Renew License](https://api.cryptlex.com/v3/docs#tag/Licenses/operation/RenewLicense) endpoint.

## Updating Expiration Date

The `expiresAt` property of the license can manually be updated to extend, shorten, or correct the license’s expiration date. The expiration date of a license can be updated from the admin portal manually or by using our REST API in automation.

* **Admin Portal:** Go to the Licenses page, click the Actions menu (three dots) next to the license, and select **Update Expiration Date** License.
* **Web API:** Send a `PATCH` request to [Update License Expiration](https://api.cryptlex.com/v3/docs#tag/Licenses/operation/UpdateExpiresAtLicense) endpoint.

***

## Migrating to Subscription Interval-Based Licensing

The steps below guide you through migrating from the legacy Validity-based model to the new Subscription Interval-based system.

### No SDK Changes Required

The migration does not require any changes in **LexActivator**, **LexFloatClient**, or **LexFloatServer**. All functionality will continue to work seamlessly.

### Using Subscription Interval in New Licenses

To use the new model for future licenses:

1. **Update the License Template**:
   * Clear the **Validity** and **Expiration Strategy** fields.
   * Set the **Subscription Interval** (e.g., `1 month` instead of `30 days`) and **Subscription Start Trigger**:
     * Use **License Creation** if the old expiration strategy was _Immediate_.
     * Use **License Activation** if it was _Delayed_.
2. **API Compatibility**:
   * The `/v3/licenses/:id/renew` endpoint continues to work as expected.
   * If you're using the `/v3/licenses/:id/extend` endpoint in scripts, replace it with the `/v3/licenses/:id/expires-at` endpoint, which takes an exact date instead of a duration.

### Updating Existing Licenses

Modifying a license template does **not** affect existing licenses. You have two options:

1. **Keep Existing Setup:**
   * Continue using **Validity** for existing licenses. Renewal and extension APIs remain supported.
2.  **Migrate to Subscription Interval**

    For each license:

    * Use the **"Update Subscription Parameters"** action from the license tables action menu.
    * Set the **Subscription Interval** and the appropriate **Start Trigger**.

**Note:** If your integration scripts use the deprecated `/v3/licenses/:id/extend endpoint`, replace it with `/v3/licenses/:id/expires-at`

> A script using the Web API is available on request to automate this update for multiple licenses.

### Summary

* No changes required in SDKs.
* Integration script updates are only needed if you use `Validity` or the `/v3/licenses/:id/extend` endpoint.
* Backward compatibility is fully maintained.

Need any help or the migration script? Contact us through [email](mailto:support@cryptlex.com?Subject=Migration%20to%20Subscription).
