# Web API

## 3.63.0 (2023-04-06)

### Added <a href="#changed" id="changed"></a>

* &#x20;`expired`, `metadata.key`, `metadata.value` and `createdAt` query params to the /v3/trial-activations endpoint.

## 3.62.0 (2023-04-04)

### Added <a href="#changed" id="changed"></a>

* &#x20;`published` and `private` query params to the /v3/releases endpoint.
* `published` query param to the /v3/releases-files endpoint.
* `action` query param to the /v3/activation-logs endpoint.

## 3.61.0 (2023-03-29)

### Added <a href="#changed" id="changed"></a>

* [/v3/webhook-event-logs](https://api.cryptlex.com/v3/docs#tag/WebhookEventLogs) endpoint to get the log of all the triggered webhook events.
* [/v3/automated-email-event-logs](https://api.cryptlex.com/v3/docs#tag/AutomatedEmailEventLogs) endpoint to get the log of all the triggered automated email events.

### Updated

* Renamed `email-templates` to `automated-emails` in login endpoint.

## 3.60.0 (2023-03-10)

### Added <a href="#changed" id="changed"></a>

* `license.maintenance-expired` and `license.maintenance-expiring-soon` events in webhooks and email templates.
* [/v3/activation-logs/export](https://api.cryptlex.com/v3/docs#tag/ActivationLogs/operation/get/v3/activation-logs/export) endpoint to export activation logs in CSV format.
* `on` (organization name) and `oa` (organization address) properties in the activation JWT response.

## 3.59.0 (2023-03-08)

### Added <a href="#changed" id="changed"></a>

* [/v3/organizations](https://api.cryptlex.com/v3/docs#tag/Organizations/operation/get/v3/organizations) endpoint to add support for organizations.

## 3.58.0 (2023-02-21)

### Added <a href="#changed" id="changed"></a>

* `lcat` (license created at) and `laat` (license activated at) properties in the activation JWT response.

## 3.57.0 (2023-02-08)

### Added <a href="#changed" id="changed"></a>

* `expiresAt` and `expiringSoon` query params to the /v3/licenses endpoint.
* `offline` property to the activation log resource.

### Fixed

* Issue causing emails sent through SendGrid to fail.

## 3.56.0 (2022-12-14)

### Added <a href="#changed" id="changed"></a>

* &#x20;`allowed` query param to the /v3/releases/update endpoint

## 3.55.0 (2022-08-26)

### Added <a href="#changed" id="changed"></a>

* [/v3/release-channels](https://api.cryptlex.com/v3/docs#tag/ReleaseChannels) endpoint to add support for adding release channels.
* [/v3/release-platforms](https://api.cryptlex.com/v3/docs#tag/ReleasePlatforms) endpoint to add support for adding release platforms

## 3.54.0 (2022-06-13)

### Added <a href="#changed" id="changed"></a>

* [/v3/maintenance-policies](https://api.cryptlex.com/v3/docs#tag/MaintenancePolicies/operation/get/v3/maintenance-policies) endpoint to add support for maintenance policies.
* [/v3/licenses/{id}/maintenance/renew](https://api.cryptlex.com/v3/docs#tag/Licenses/operation/post/v3/licenses/%7Bid%7D/maintenance/renew) endpoint to add support for renewing license maintenance.
* [/v3/licenses/{id}/maintenance/extend](https://api.cryptlex.com/v3/docs#tag/Licenses/operation/post/v3/licenses/%7Bid%7D/maintenance/extend) endpoint to add support for extending license maintenance.
* `maintenancePolicyId` property to the license resource.
* `currentReleaseVersion` property to the license resource.
* `maxAllowedReleaseVersion` property to the license resource.
* `releaseVersion` property to the activation resource.

## 3.53.0 (2022-06-01)

### Added <a href="#changed" id="changed"></a>

* [/v3/activations/{id}deactivate](https://api.cryptlex.com/v3/docs#tag/Activations/operation/post/v3/activations/%7Bid%7D/deactivate) endpoint for secure deactivation of activations.
* Added `accountId` in login endpoint.
* Added `accountId` in activation, trial activation and deactivation endpoints.
* Added `accountId` in release update and latest endpoint.
* Added `accountId` in release download URL.

### Updated

* Renamed `companyId` to `accountAlias` in login endpoint.

## 3.52.0 (2022-03-28)

### Added <a href="#changed" id="changed"></a>

* /v3/sending-domains endpoint to add support for DMARC compliant emails.

## 3.51.0 (2022-02-11)

### Added <a href="#changed" id="changed"></a>

* `resourceId` query param to event logs.

## 3.50.0 (2022-01-27)

### Added <a href="#changed" id="changed"></a>

* `disableValidationCheck` property to the license resource.

## 3.49.0 (2021-12-01)

### Added <a href="#changed" id="changed"></a>

* `changes` property to the event log resource.

## 3.48.0 (2021-11-17)

### Added <a href="#changed" id="changed"></a>

* `allowClientLeaseDuration` property to the license resource.

## 3.47.0 (2021-11-01)

### Added <a href="#changed" id="changed"></a>

* [/v3/product-versions](https://api.cryptlex.com/v3/docs#tag/ProductVersions) endpoint to add support for product versions.
* [/v3/feature-flags](https://api.cryptlex.com/v3/docs#tag/FeatureFlags) endpoint to add support for feature flags.

## 3.46.0 (2021-10-25)

### Added <a href="#changed" id="changed"></a>

* `user.created` event in the email templates.
* `user.reset-password-request` event in the email templates.

## 3.45.0 (2021-10-07)

### Added <a href="#changed" id="changed"></a>

* `private` property to the release resource.
* `license.deleted` event in the webhooks and email templates.

## 3.44.0 (2021-09-20)

### Added <a href="#changed" id="changed"></a>

* query operators support.
* `user.company` query param to /v3/licenses endpoint.
* `activation.appVersion` query param to /v3/users endpoint.

### Deprecated

* `createdAfter` and `createdBefore` in /v3/licenses, /v3/users, /v3/activation-logs endpoints. These can be replaced with `createdAt[gt]` and `createdAt[lt]` respectively.
* `lastSeenAfter` and `lastSeenBefore` in /v3/users endpoint. These can be replaced with `lastSeenAt[gt]` and `lastSeenAt[lt]` respectively.
* `metadataKey` and `metadataValue` in /v3/licenses and /v3/users endpoints. These can be replaced with `metadata.key` and `metadata.value` respectively.
* `email` in /v3/licenses endpoint. This can be replaced with `user.email`.

## 3.43.0 (2021-08-05)

### Added <a href="#changed" id="changed"></a>

* `createdAfter` and `createdBefore` query params to [/v3/activation-logs](https://api.cryptlex.com/v3/docs#tag/ActivationLogs) endpoint.

## 3.42.0 (2021-05-19)

### Added <a href="#changed" id="changed"></a>

* `allowCustomerPortalAccess` property to the user resource.

## 3.41.0 (2021-03-18)

### Added <a href="#changed" id="changed"></a>

* `offline` property to the activation resource.

## 3.40.0 (2021-03-10)

### Added <a href="#changed" id="changed"></a>

* [/v3/users/export](https://api.cryptlex.com/v3/docs#operation/get/v3/users/export) endpoint to add support for exporting the users in CSV format.
* [/v3/trial-activations/export](https://api.cryptlex.com/v3/docs#operation/get/v3/trial-activations/export) endpoint to add support for exporting the trial activations in the CSV format.

## 3.39.0 (2021-02-10)

### Added <a href="#changed" id="changed"></a>

* `additionalUserIds` property to the license resource.

## 3.38.0 (2021-01-28)

### Added <a href="#changed" id="changed"></a>

* [/v3/licenses/meter-attributes/{id}/reset](https://api.cryptlex.com/v3/docs#operation/post/v3/licenses/meter-attributes/{id}/reset) endpoint to add support for resetting the meter attributes.
* [/v3/licenses/meter-attributes/{id}](https://api.cryptlex.com/v3/docs#operation/delete/v3/licenses/meter-attributes/{id}) endpoint to add support for deleting the meter attributes.
* [/v3/licenses/metadata/{id}](https://api.cryptlex.com/v3/docs#operation/delete/v3/licenses/metadata/{id}) endpoint to add support for deleting the metadata fields.

## 3.37.0 (2021-01-06)

### Added <a href="#changed" id="changed"></a>

* `appVersion` property to the activation log resource.

## 3.36.0 (2020-12-28)

### Added <a href="#changed" id="changed"></a>

* `floating` property to the meter attribute resource.
* `allowContainerActivation` property to the license and trial policy resources.

## 3.35.0 (2020-12-22)

### Added <a href="#changed" id="changed"></a>

* Support for caching to improve performance.

## 3.34.0 (2020-12-01)

### Updated <a href="#changed" id="changed"></a>

* Meter attributes are now persistent by default.

## 3.33.0 (2020-11-20)

### Added <a href="#changed" id="changed"></a>

* `visible` property to the meter attribute resource.

## 3.32.0 (2020-09-23)

### Added <a href="#changed" id="changed"></a>

* `allowedIpRanges` property to the license resource.

## 3.31.0 (2020-07-07)

### Added <a href="#changed" id="changed"></a>

* SAML SSO support.

## 3.30.0 (2020-06-06)

### Added <a href="#changed" id="changed"></a>

* `cc` and `bcc` properties to the email templates.

## 3.29.0 (2020-06-02)

### Added <a href="#changed" id="changed"></a>

* `expiringSoonEventOffset` property to the license policy and the license resources.

## 3.28.0 (2020-05-05)

### Added <a href="#changed" id="changed"></a>

* `metadataKey` and `metadataValue` query params to [/v3/activations](https://api.cryptlex.com/v3/docs#operation/get/v3/activations) endpoint.

## 3.27.0 (2020-04-21)

### Added <a href="#changed" id="changed"></a>

* `allowedIpRange` property to the license resource.

## 3.26.0 (2020-03-28)

### Added <a href="#changed" id="changed"></a>

* [/v3/email-templates](https://api.cryptlex.com/v3/docs#tag/EmailTemplates) endpoint to add support for [email templates](broken-reference).

## 3.25.0 (2020-01-25)

### Added <a href="#changed" id="changed"></a>

* `keyPattern` property to the license policy resource.

## 3.24.0 (2019-11-18)

### Added <a href="#changed" id="changed"></a>

* `grossUses` property to the license meter attributes.
* `metadataKey` and `metadataValue` query params to the /v3/users endpoint.

## 3.23.0 (2019-10-20)

### Fixed <a href="#changed" id="changed"></a>

* Some minor bug fixes and improvements.

## 3.22.0 (2019-09-16)

### Added <a href="#changed" id="changed"></a>

* `product.displayName` property to the user release resource.

## 3.21.0 (2019-07-23)

### Added <a href="#changed" id="changed"></a>

* `disableGeoLocation` property to the license policy, trial policy and license resources, to prevent storing IP and location data.
* `downloads` property to the release file resource, to track number of downloads.

## 3.20.0 (2019-05-15)

### Added <a href="#changed" id="changed"></a>

* `requiredMeterAttributes` property to the license policy resource, to enforce meter attributes schema for the licenses.
* `meterAttributes` property to the license resource.

## 3.19.0 (2019-04-30)

### Added <a href="#changed" id="changed"></a>

* `requireAuthentication` property to the license resource, to enforce user authentication for license activation.

## 3.18.0 (2019-04-15)

### Added <a href="#changed" id="changed"></a>

* `resellerId` property to the license resource.
* `tags` property to the user resource.

## 3.17.0 (2019-04-12)

### Added <a href="#changed" id="changed"></a>

* [/v3/docs#tag/ReleaseFiles](https://api.cryptlex.com/v3/docs#tag/ReleaseFiles) endpoints to add support for external files in the releases.

## 3.16.0 (2019-04-10)

### Added <a href="#changed" id="changed"></a>

* [/v3/accounts/login-google](https://api.cryptlex.com/v3/docs#operation/V3AccountsLoginPost) endpoint to enable login using Google SSO.

## 3.15.0 (2019-03-25)

### Added <a href="#changed" id="changed"></a>

* Support for [per-instance](https://docs.cryptlex.com/license-management/license-policies#leasing-strategy) leasing strategy for hosted-floating license type.

## 3.14.0 (2019-03-14)

### Added <a href="#changed" id="changed"></a>

* [/v3/me/releases](https://api.cryptlex.com/v3/docs#operation/get/v3/me/releases) endpoint to display releases in the dashboard.

## 3.13.0 (2019-03-05)

### Added <a href="#changed" id="changed"></a>

* `license.expired` and `license.expiring-soon` events to webhooks.
* `account.logged-in` event to event log.
* Partial version comparison in [update](https://docs.cryptlex.com/release-management/distributing-releases#downloading-an-update) API endpoint for ignoring patch and build updates.

## 3.12.0 (2019-02-23)

### Added <a href="#changed" id="changed"></a>

* `displayName` to [products](https://api.cryptlex.com/v3/docs#operation/V3ProductsGet) resource.

## 3.11.0 (2019-02-20)

### Added <a href="#changed" id="changed"></a>

* [/v3/status](https://api.cryptlex.com/v3/status) health check endpoint.
* Dynamic origin for password reset mails.
* `customDomain`, `website`, `logoUrl`, `faviconUrl` to [accounts](https://api.cryptlex.com/v3/docs#operation/V3AccountsByIdGet) resource.

## 3.10.0 (2018-12-17)

### Added <a href="#changed" id="changed"></a>

* `leasingStrategy` property to [licenses](https://api.cryptlex.com/v3/docs#operation/V3LicensesByIdGet) resource.
* `company` query param to [users](https://api.cryptlex.com/v3/docs#operation/V3UsersGet) resource.

## 3.9.0 (2018-12-06)

### Added <a href="#changed" id="changed"></a>

* Support for referrals.
* `role` property to [users](https://api.cryptlex.com/v3/docs#operation/V3UsersPost) resource deprecating `roles` property.

## 3.8.0 (2018-10-12)

### Added <a href="#changed" id="changed"></a>

* [/v3/me/2fa-secret](https://api.cryptlex.com/v3/docs#operation/V3Me2fa-secretPost) and [/v3/me/2fa-recovery-codes](https://api.cryptlex.com/v3/docs#operation/V3Me2fa-recovery-codesPost) endpoints to allow for two factor authentication.

## 3.7.0 (2018-09-12)

### Added <a href="#changed" id="changed"></a>

* [/v3/trial-activations/offline-activate](https://api.cryptlex.com/v3/docs#operation/V3Trial-activationsOffline-activatePost) endpoint to allow for offline trial activations.

## 3.6.0 (2018-09-09)

### Added <a href="#changed" id="changed"></a>

* Support for bank deposits through dashboard as alternative for credit cards.

## 3.5.0 (2018-08-06)

### Added <a href="#changed" id="changed"></a>

* `allowedClockOffset` property to license policies and licenses which can be used to allow license and trial activations on machines where system clocks run behind the network time.
* [/v3/analytics/activations/app-version](https://api.cryptlex.com/v3/docs#operation/V3AnalyticsActivationsApp-versionGet) endpoint to retrieve activations by app version.

## 3.4.0 (2018-06-25)

### Added <a href="#changed" id="changed"></a>

* [Distribution API](https://api.cryptlex.com/v3/docs#tag/Releases) for secure distribution of software applications and release management.
* [/v3/users/:id/reset-password-token](https://api.cryptlex.com/v3/docs#operation/V3UsersByIdReset-password-tokenPost) endpoint to allow implementation of forgot password functionality for custom branded portals.

## 3.3.0 (2018-06-09)

### Added <a href="#changed" id="changed"></a>

* [/v3/licenses/:id/extend](https://api.cryptlex.com/v3/docs#operation/V3LicensesByIdExtendPost) endpoint to allow extension of licenses. Before this only license renewal was allowed.

### Fixed

* Some minor bug fixes.

## 3.2.0 (2018-05-28)

### Added <a href="#changed" id="changed"></a>

* [/v3/me](https://api.cryptlex.com/v3/docs#operation/V3MeGet) and [/v3/me/licenses](https://api.cryptlex.com/v3/docs#operation/V3MeLicensesGet) endpoints for customer portal.

### Fixed

* Some minor bug fixes.

## 3.1.0 (2018-05-21)

### Added <a href="#changed" id="changed"></a>

* `licensePolicyId` property to licenses which can be used to override the default license policy of a license, inherited through product.
* `requiredMetadataKeys` property to license policies to make it must for a license to have required metadata keys when it is created. The metadata keys will automatically appear for licenses in the dashboard.

### Fixed

* Some minor bug fixes and improvements.

## 3.0.1 (2018-05-18) <a href="#3-0-0-2018-05-03" id="3-0-0-2018-05-03"></a>

### Changed <a href="#changed" id="changed"></a>

* Each license you create is counted as an activation irrespective of whether it is activated or not (as before). But if license allows more than one activation, then those are only counted when used.
* `allowedActivations` property in license policies and licenses can now be set to `0` also, to allow unlimited activations for any license.
* For on-premise floating licenses `allowedFloatingClients` are no more counted as activations, that means floating licenses got more cheaper.

### Fixed <a href="#deleted" id="deleted"></a>

* Some issues in floating licenses.
* Other minor bug fixes.

## 3.0.0 (2018-05-03)

### Added

* Completely new REST API
* Beautiful API [docs](https://api.cryptlex.com/v3/docs)
