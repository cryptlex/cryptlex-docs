---
description: All notable changes to LexActivator are documented here.
---

# LexActivator

## 3.3.1 \(2018-12-17\)

### Fixed

* A bug preventing changing of permission flag from LA\_SYSTEM to LA\_USER when former is set first.

## 3.3.0 \(2018-09-12\)

### Added

* `GenerateOfflineTrialActivationRequest()` and `ActivateTrialOffline()` functions to allow for offline trial activations.

### Updated <a id="updated"></a>

* Wrappers for languages have been updated with `GenerateOfflineTrialActivationRequest()` and `ActivateTrialOffline()`  API functions. Please update your wrappers using the latest code on [Github](https://github.com/cryptlex).

## 3.2.0 \(2018-08-20\)

### Added

* `GetLicenseType()` function to get the license type \(node-locked or hosted-floating\).

### Updated

* Wrappers for languages have been updated with `GetLicenseType()` API function. Please update your wrappers using the latest code on [Github](https://github.com/cryptlex).

## 3.1.0 \(2018-08-06\)

### Added

* Support for clock offset property set for the licenses in the dashboard, which can be used to allow license and trial activations on machines where system clocks run behind the network time.

### Changed

* Time tampering detection threshold has been increased to around one hour to allow for daylight savings and minor changes in the system time.
* On time tampering detection instead of returning `LA_E_TIME` it now returns `LA_E_TIME_MODIFIED`. 

  Now `LA_E_TIME` is returned only when the system time is behind the network time by more than the allowed clock offset.

### Updated

* Wrappers for languages have been updated with `LA_E_TIME_MODIFIED` status code. Please update your wrappers using the latest code on [Github](https://github.com/cryptlex).

## 3.0.5 \(2018-07-21\)

### Fixed

* A bug causing causing crash on few Windows machines, with WMIC service not running.

## 3.0.4 \(2018-07-18\)

### Fixed

* A bug causing causing crash on Linux, if license is deleted server side.

## 3.0.3 \(2018-06-14\)

### Fixed

* A bug causing insufficient system permissions error on first run on Linux.

## 3.0.2 \(2018-05-30\)

### Fixed

* A network SSL issue causing activations to fail for few proxies.

## 3.0.1 \(2018-05-10\)

### Fixed

* A network issue causing activations to fail.

## 3.0.0 \(2018-05-03\)

### Added

* `SetProductData()` function
* `SetLicenseCallback()` function
* `SetTrialActivationMetadata()` function
* `SetAppVersion()` function
* `GetProductMetadata()` function
* `GetLicenseUserEmail()` function
* `GetLicenseUserName()` function
* `GetTrialActivationMetadata()` function
* `GetTrialExpiryDate()` function
* `GetTrialId()` function
* `GetLocalTrialExpiryDate()` function
* `IsLocalTrialGenuine()` function
* `ExtendLocalTrial()` function
* `Reset()` function

### Changed

* All status codes have been updated
* Renamed `SetVersionGUID()` function to `SetProductId()`
* Renamed `SetProductKey()` function to `SetLicenseKey()`
* Renamed `SetExtraActivationData()` function to `SetActivationMetadata()`
* Renamed `ActivateProduct()` function to `ActivateLicense()`
* Renamed `DeactivateProduct()` function to `DeactivateLicense()`
* Renamed `ActivateProductOffline()` function to `ActivateLicenseOffline()`
* Renamed `IsProductGenuine()` function to `IsLicenseGenuine()`
* Renamed `IsProductActivated()` function to `IsLicenseValid()`
* Renamed `GetExtraActivationData()` function to `GetActivationMetadata()`
* Renamed `GetCustomLicenseField()` function to `GetLicenseMetadata()`
* Renamed `GetProductKeyExpiryDate()` function to `GetLicenseExpiryDate()`
* Renamed `InitializeTrial()` function to `ActivateLocalTrial()`

### Deleted

* `GetDaysLeftToExpiration()` function
* `SetTrialKey()` function
* `ExtendTrial()` function
* `GetTrialDaysLeft()` function
* `SetDayIntervalForServerCheck()` function
* `SetGracePeriodForNetworkError()` function
* `SetUserLock()` function

## 2.9.6 \(2017-11-19\)

### Added

* `GetProductKeyExpiryDate()` function to get the product key expiry timestamp.
* Support for Linux ARMv8 64 bit architecture

## 2.9.5 \(2017-10-19\)

### Fixed

* Bug preventing grace period not to expire on no server sync

## 2.9.4 \(2017-09-23\)

### Fixed

* Bug causing incorrect detection of Hyper-V

## 2.9.3 \(2017-09-09\)

### Fixed

* Bug causing grace period not to expire
* Regression causing LA\_EXPIRED to return for deactivated licenses

## 2.9.2 \(2017-08-28\)

### Fixed

* A major bug causing LA\_FAIL status to be returned for activated products

## 2.9.0 \(2017-07-03\)

### Added

* clang build for macOS

### Changed

* `ActivateProduct()` function now returns \(throws\) LA\_E\_ACT\_LIMIT error \(exception\) if activation limit is reached
* `IsProductGenuine()` function won't reactivate the product key, if deactivated server side

## 2.8.1 \(2017-05-21\)

### Fixed

* Embedded version

## 2.8.0 \(2017-05-16\)

### Added

* Support for changing product version without restart

### Fixed

* Minor bug fixes

## 2.7.1 \(2017-04-05\)

### Fixed

* GCE VM detection bug

## 2.7.0 \(2017-03-04\)

### Added

* Support for Linux ARMv5 and ARMv7 architectures
* Server sync for revoked licenses

### Fixed

* Minor bug fixes

## 2.6.1 \(2017-01-26\)

### Fixed

* A memory leak in `IsProductGenuine()` function if being invoked periodically

## 2.6.0 \(2017-01-22\)

### Changed

* `DeactivateProduct()` now returns LA\_E\_DEACT\_LIMIT instead of LA\_FAIL if deactivation limit is reached for the key

### Fixed

* Minor bug fixes

## 2.5.1 \(2016-12-27\)

### Changed

* All setter functions other than `SetVersionGUID()` are now only needed at the time of activation
* `DeactivateProduct()` now deactivates the product even if product key is expired

### Fixed

* AWS VM detection bug

## 2.4.0 \(2016-12-12\)

### Added

* `SetUserLock()` function to support user locked licenses.

### Changed

* `DeactivateProduct()` function now deactivates the product locally even if product key is already deactivated server side, and LA\_FAIL is returned.

## 2.3.0 \(2016-05-22\)

### Fixed

* A minor bug in offline activation.
* A minor bug in VM activation.

## 2.2.1 \(2016-03-21\)

### Added

* `GetExtraActivationData()` function to get the value of the extra activation data.
* `GetDaysLeftToExpiration()` function to get the number of remaining days after which the license expires.

