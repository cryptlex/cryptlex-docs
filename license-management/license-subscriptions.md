# License Subscriptions

## Subscriptions

In Cryptlex, a subscription is a time-based licensing model where a license is valid for a specific duration (e.g., months or years). It offers flexible access control, making it ideal for recurring billing and time-limited access. A subscription can be configured by setting a subscription interval or specifying an exact expiration date.

## Adding a Subscription to a License

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
