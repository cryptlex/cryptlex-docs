# Web API

## 3.5.0 \(2018-07-06\)

### Added {#changed}

* `allowedClockOffset` property to license policies and licenses which can be used to allow license and trial activations on machines where system clocks run behind the network time.
* [/v3/analytics/activations/app-version](https://api.cryptlex.com/v3/docs#operation/V3AnalyticsActivationsApp-versionGet) endpoint to retrieve activations by app version.

## 3.4.0 \(2018-06-25\)

### Added {#changed}

* [Distribution API](https://api.cryptlex.com/v3/docs#tag/Releases) for secure distribution of software applications and release management.
* [/v3/users/:id/reset-password-token](https://api.cryptlex.com/v3/docs#operation/V3UsersByIdReset-password-tokenPost) endpoint to allow implementation of forgot password functionality for custom branded portals.

## 3.3.0 \(2018-06-09\)

### Added {#changed}

* [/v3/licenses/:id/extend](https://api.cryptlex.com/v3/docs#operation/V3LicensesByIdExtendPost) endpoint to allow extension of licenses. Before this only license renewal was allowed.

### Fixed

* Some minor bug fixes.

## 3.2.0 \(2018-05-28\)

### Added {#changed}

* [/v3/me](https://api.cryptlex.com/v3/docs#operation/V3MeGet) and [/v3/me/licenses](https://api.cryptlex.com/v3/docs#operation/V3MeLicensesGet) endpoints for customer portal.

### Fixed

* Some minor bug fixes.

## 3.1.0 \(2018-05-21\)

### Added {#changed}

* `licensePolicyId` property to licenses which can be used to override the default license policy of a license, inherited through product.
* `requiredMetadataKeys` property to license policies to make it must for a license to have required metadata keys when it is created. The metadata keys will automatically appear for licenses in the dashboard.

### Fixed

* Some minor bug fixes and improvements.

## 3.0.1 \(2018-05-18\) {#3-0-0-2018-05-03}

### Changed {#changed}

* Each license you create is counted as an activation irrespective of whether it is activated or not \(as before\). But if license allows more than one activation, then those are only counted when used.
* `allowedActivations` property in license policies and licenses can now be set to `0` also, to allow unlimited activations for any license.
* For on-premise floating licenses `allowedFloatingClients` are no more counted as activations, that means floating licenses got more cheaper.

### Fixed {#deleted}

* Some issues in floating licenses.
* Other minor bug fixes.

## 3.0.0 \(2018-05-03\)

### Added

* Completely new REST API
* Beautiful API [docs](https://api.cryptlex.com/v3/docs)

## Previous Versions

### Let's move on...

