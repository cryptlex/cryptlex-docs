# Web API

## 3.42.0 \(2021-05-19\)

### Added <a id="changed"></a>

* `allowCustomerPortalAccess` property to the user resource.

## 3.41.0 \(2021-03-18\)

### Added <a id="changed"></a>

* `offline` property to the activation resource.

## 3.40.0 \(2021-03-10\)

### Added <a id="changed"></a>

* [/v3/users/export](https://api.cryptlex.com/v3/docs#operation/get/v3/users/export) endpoint to add support for exporting the users in CSV format.
* [/v3/trial-activations/export](https://api.cryptlex.com/v3/docs#operation/get/v3/trial-activations/export) endpoint to add support for exporting the trial activations in the CSV format.

## 3.39.0 \(2021-02-10\)

### Added <a id="changed"></a>

* `additionalUserIds` property to the license resource.

## 3.38.0 \(2021-01-28\)

### Added <a id="changed"></a>

* [/v3/licenses/meter-attributes/{id}/reset](https://api.cryptlex.com/v3/docs#operation/post/v3/licenses/meter-attributes/{id}/reset) endpoint to add support for resetting the meter attributes.
* [/v3/licenses/meter-attributes/{id}](https://api.cryptlex.com/v3/docs#operation/delete/v3/licenses/meter-attributes/{id}) endpoint to add support for deleting the meter attributes.
* [/v3/licenses/metadata/{id}](https://api.cryptlex.com/v3/docs#operation/delete/v3/licenses/metadata/{id}) endpoint to add support for deleting the metadata fields.

## 3.37.0 \(2021-01-06\)

### Added <a id="changed"></a>

* `appVersion` property to the activation log resource.

## 3.36.0 \(2020-12-28\)

### Added <a id="changed"></a>

* `floating` property to the meter attribute resource.
* `allowContainerActivation` property to the license and trial policy resources.

## 3.35.0 \(2020-12-22\)

### Added <a id="changed"></a>

* Support for caching to improve performance.

## 3.34.0 \(2020-12-01\)

### Updated <a id="changed"></a>

* Meter attributes are now persistent by default.

## 3.33.0 \(2020-11-20\)

### Added <a id="changed"></a>

* `visible` property to the meter attribute resource.

## 3.32.0 \(2020-09-23\)

### Added <a id="changed"></a>

* `allowedIpRanges` property to the license resource.

## 3.31.0 \(2020-07-07\)

### Added <a id="changed"></a>

* SAML SSO support.

## 3.30.0 \(2020-06-06\)

### Added <a id="changed"></a>

* `cc` and `bcc` properties to the email templates.

## 3.29.0 \(2020-06-02\)

### Added <a id="changed"></a>

* `expiringSoonEventOffset` property to the license policy and the license resources.

## 3.28.0 \(2020-05-05\)

### Added <a id="changed"></a>

* `metadataKey` and `metadataValue` query params to [/v3/activations](https://api.cryptlex.com/v3/docs#operation/get/v3/activations) endpoint.

## 3.27.0 \(2020-04-21\)

### Added <a id="changed"></a>

* `allowedIpRange` property to the license resource.

## 3.26.0 \(2020-03-28\)

### Added <a id="changed"></a>

* [/v3/email-templates](https://api.cryptlex.com/v3/docs#tag/EmailTemplates) endpoint to add support for [email templates](../email-templates.md).

## 3.25.0 \(2020-01-25\)

### Added <a id="changed"></a>

* `keyPattern` property to the license policy resource.

## 3.24.0 \(2019-11-18\)

### Added <a id="changed"></a>

* `grossUses` property to the license meter attributes.
* `metadataKey` and `metadataValue` query params to the /v3/users endpoint.

## 3.23.0 \(2019-10-20\)

### Fixed <a id="changed"></a>

* Some minor bug fixes and improvements.

## 3.22.0 \(2019-09-16\)

### Added <a id="changed"></a>

* `product.displayName` property to the user release resource.

## 3.21.0 \(2019-07-23\)

### Added <a id="changed"></a>

* `disableGeoLocation` property to the license policy, trial policy and license resources, to prevent storing IP and location data.
* `downloads` property to the release file resource, to track number of downloads.

## 3.20.0 \(2019-05-15\)

### Added <a id="changed"></a>

* `requiredMeterAttributes` property to the license policy resource, to enforce meter attributes schema for the licenses.
* `meterAttributes` property to the license resource.

## 3.19.0 \(2019-04-30\)

### Added <a id="changed"></a>

* `requireAuthentication` property to the license resource, to enforce user authentication for license activation.

## 3.18.0 \(2019-04-15\)

### Added <a id="changed"></a>

* `resellerId` property to the license resource.
* `tags` property to the user resource.

## 3.17.0 \(2019-04-12\)

### Added <a id="changed"></a>

* [/v3/docs\#tag/ReleaseFiles](https://api.cryptlex.com/v3/docs#tag/ReleaseFiles) endpoints to add support for external files in the releases.

## 3.16.0 \(2019-04-10\)

### Added <a id="changed"></a>

* [/v3/accounts/login-google](https://api.cryptlex.com/v3/docs#operation/V3AccountsLoginPost) endpoint to enable login using Google SSO.

## 3.15.0 \(2019-03-25\)

### Added <a id="changed"></a>

* Support for [per-instance](https://docs.cryptlex.com/license-management/license-policies#leasing-strategy) leasing strategy for hosted-floating license type.

## 3.14.0 \(2019-03-14\)

### Added <a id="changed"></a>

* [/v3/me/releases](https://api.cryptlex.com/v3/docs#operation/get/v3/me/releases) endpoint to display releases in the dashboard.

## 3.13.0 \(2019-03-05\)

### Added <a id="changed"></a>

* `license.expired` and `license.expiring-soon` events to webhooks.
* `account.logged-in` event to event log.
* Partial version comparison in [update](https://docs.cryptlex.com/release-management/distributing-releases#downloading-an-update) API endpoint for ignoring patch and build updates.

## 3.12.0 \(2019-02-23\)

### Added <a id="changed"></a>

* `displayName` to [products](https://api.cryptlex.com/v3/docs#operation/V3ProductsGet) resource.

## 3.11.0 \(2019-02-20\)

### Added <a id="changed"></a>

* [/v3/status](https://api.cryptlex.com/v3/status) health check endpoint.
* Dynamic origin for password reset mails.
* `customDomain`, `website`, `logoUrl`, `faviconUrl` to [accounts](https://api.cryptlex.com/v3/docs#operation/V3AccountsByIdGet) resource.

## 3.10.0 \(2018-12-17\)

### Added <a id="changed"></a>

* `leasingStrategy` property to [licenses](https://api.cryptlex.com/v3/docs#operation/V3LicensesByIdGet) resource.
* `company` query param to [users](https://api.cryptlex.com/v3/docs#operation/V3UsersGet) resource.

## 3.9.0 \(2018-12-06\)

### Added <a id="changed"></a>

* Support for referrals.
* `role` property to [users](https://api.cryptlex.com/v3/docs#operation/V3UsersPost) resource deprecating `roles` property.

## 3.8.0 \(2018-10-12\)

### Added <a id="changed"></a>

* [/v3/me/2fa-secret](https://api.cryptlex.com/v3/docs#operation/V3Me2fa-secretPost) and [/v3/me/2fa-recovery-codes](https://api.cryptlex.com/v3/docs#operation/V3Me2fa-recovery-codesPost) endpoints to allow for two factor authentication.

## 3.7.0 \(2018-09-12\)

### Added <a id="changed"></a>

* [/v3/trial-activations/offline-activate](https://api.cryptlex.com/v3/docs#operation/V3Trial-activationsOffline-activatePost) endpoint to allow for offline trial activations.

## 3.6.0 \(2018-09-09\)

### Added <a id="changed"></a>

* Support for bank deposits through dashboard as alternative for credit cards.

## 3.5.0 \(2018-08-06\)

### Added <a id="changed"></a>

* `allowedClockOffset` property to license policies and licenses which can be used to allow license and trial activations on machines where system clocks run behind the network time.
* [/v3/analytics/activations/app-version](https://api.cryptlex.com/v3/docs#operation/V3AnalyticsActivationsApp-versionGet) endpoint to retrieve activations by app version.

## 3.4.0 \(2018-06-25\)

### Added <a id="changed"></a>

* [Distribution API](https://api.cryptlex.com/v3/docs#tag/Releases) for secure distribution of software applications and release management.
* [/v3/users/:id/reset-password-token](https://api.cryptlex.com/v3/docs#operation/V3UsersByIdReset-password-tokenPost) endpoint to allow implementation of forgot password functionality for custom branded portals.

## 3.3.0 \(2018-06-09\)

### Added <a id="changed"></a>

* [/v3/licenses/:id/extend](https://api.cryptlex.com/v3/docs#operation/V3LicensesByIdExtendPost) endpoint to allow extension of licenses. Before this only license renewal was allowed.

### Fixed

* Some minor bug fixes.

## 3.2.0 \(2018-05-28\)

### Added <a id="changed"></a>

* [/v3/me](https://api.cryptlex.com/v3/docs#operation/V3MeGet) and [/v3/me/licenses](https://api.cryptlex.com/v3/docs#operation/V3MeLicensesGet) endpoints for customer portal.

### Fixed

* Some minor bug fixes.

## 3.1.0 \(2018-05-21\)

### Added <a id="changed"></a>

* `licensePolicyId` property to licenses which can be used to override the default license policy of a license, inherited through product.
* `requiredMetadataKeys` property to license policies to make it must for a license to have required metadata keys when it is created. The metadata keys will automatically appear for licenses in the dashboard.

### Fixed

* Some minor bug fixes and improvements.

## 3.0.1 \(2018-05-18\) <a id="3-0-0-2018-05-03"></a>

### Changed <a id="changed"></a>

* Each license you create is counted as an activation irrespective of whether it is activated or not \(as before\). But if license allows more than one activation, then those are only counted when used.
* `allowedActivations` property in license policies and licenses can now be set to `0` also, to allow unlimited activations for any license.
* For on-premise floating licenses `allowedFloatingClients` are no more counted as activations, that means floating licenses got more cheaper.

### Fixed <a id="deleted"></a>

* Some issues in floating licenses.
* Other minor bug fixes.

## 3.0.0 \(2018-05-03\)

### Added

* Completely new REST API
* Beautiful API [docs](https://api.cryptlex.com/v3/docs)

