# Web API

## 3.10.0 \(2018-12-17\)

### Added <a id="changed"></a>

* `leasingStrategy` property to [licenses](https://api.cryptlex.com/v3/docs#operation/V3LicensesByIdGet) resource.
* `company` query param to [users](https://api.cryptlex.com/v3/docs#operation/V3UsersGet) resource

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

