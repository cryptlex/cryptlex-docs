# LexActivator

## 3.26.0 (2024-02-09)

### Added

* `GetLicenseAllowedDeactivations()` function to get the allowed deactivations of the license.
* `GetLicenseTotalDeactivations()` function to get the total deactivations of the license.

### Fixed

* Minor bug fix.

## 3.25.2 (2024-01-17)

### Fixed

* Minor bug fix.

## 3.25.1 (2024-01-02)

### Fixed

* Minor bug fix.

## 3.25.0 (2023-12-01)

### Added

* `GetActivationId()` function to get the activation ID.
* Added support for EU data center.

## 3.24.1 (2023-10-10)

### Fixed

* Minor bug fix.

## 3.24.0 (2023-09-27)

### Added

* `AuthenticateUserWithIdToken()`function to authenticate the user via the OIDC ID token.

## 3.23.3 (2023-09-23)

### Fixed

* Minor bug fix.

## 3.23.2 (2023-09-21)

### Fixed

* Minor bug fix.

## 3.23.1 (2023-09-05)

### Fixed

* Added missing check for the existence of meter attribute before incrementing, decrementing and resetting the count.
* Added missing server sync in the case when `IsLicenseGenuine()` function returns `LA_E_RELEASE_VERSION_NOT_ALLOWED` error code.

## 3.23.0 (2023-08-10)

### Added

* `SetTwoFactorAuthenticationCode()` function to authenticate the users with 2FA enabled.

### Fixed

* Fingerprint-related issues in Android devices.

## 3.22.0 (2023-07-31)

### Added

* `AuthenticateUser()` function to authenticate the user.
* `GetUserLicenses()` function to get the licenses linked with the user.
* `GetLicenseCreationDate()` function to get the creation date timestamp of the license.
* `GetLicenseActivationDate()` function to get the activation date timestamp of the license.

## 3.21.5 (2023-06-23)

### Fixed

* Minor bug fix.

## 3.21.4 (2023-06-03)

### Fixed

* Activation validation issue due to a very large number of metadata fields.

## 3.21.3 (2023-05-31)

### Fixed

* Crash in some OEM Android devices due to GSF ID.
* Fingerprint-related issue in Android devices of the same make.

## 3.21.2 (2023-04-17)

### Fixed

* Minor bug fixes.

## 3.21.1 (2023-04-10)

### Fixed

* Minor bug fixes.

## 3.21.0 (2023-04-06)

### Added

* `GetLicenseOrganizationName()` function to get the license organization name.
* `GetLicenseOrganizationAddress()` function to get the license organization address.
* `CheckReleaseUpdate()` function to check whether a new release is available for the product. It also determines if the update is allowed or not and provides the release object if a new release is available.

### Deprecated

* `CheckForReleaseUpdate()` function has been deprecated in favour of `CheckReleaseUpdate()` function.

## 3.20.9 (2023-02-10)

### Fixed

* False positive container detection on some Linux distributions.

## 3.20.8 (2023-02-10)

### Fixed

* Container detection issue on recent Linux distributions.&#x20;

## 3.20.7 (2022-12-01)

### Fixed

* Encoding issue in `GetProductVersionName()` function.&#x20;

## 3.20.6 (2022-11-22)

### Fixed

* Issue preventing detection of Windows Server 2022.

## 3.20.5 (2022-11-17)

### Fixed

* NTLM proxy authentication issue.

## 3.20.4 (2022-11-14)

### Fixed

* Fingerprint issue in Android trial activations.

## 3.20.3 (2022-11-11)

### Fixed

* Missing OS version in the case of some Windows server machines.

## 3.20.2 (2022-11-04)

### Fixed

* Minor bug fixes.

## 3.20.1 (2022-11-02)

### Fixed

* Minor bug fixes.

## 3.20.0 (2022-11-01)

### Added

* `GetLicenseMaxAllowedReleaseVersion()`  function to get the maximum allowed release version of the license.
* `SetReleaseChannel()`  function to set the release channel e.g. stable, beta etc. of the application.
* `SetReleasePlatform()`  function to set the release platform e.g. windows, macos, linux etc. of the application.
* `SetReleasePublishedDate()` function to set the release published date of your application.

## 3.19.2 (2022-08-10)

### Fixed

* Removed external `libcurl` dependency in Linux `musl` build

## 3.19.1 (2022-06-18)

### Fixed

* Minor bug fixes.

## 3.19.0 (2022-06-14)

### Added

* `GetActivationMode()`  function to get the mode of activation (online or offline).
* `GetLicenseMaintenanceExpiryDate()`  function to get the expiry date of maintenance.
* `SetReleaseVersion()`  function to set the release version.

## 3.18.2 (2022-04-25)

### Fixed

* Issues related to device fingerprinting on Android.

## 3.18.1 (2022-04-05)

### Updated

* Dropped dependency on system `libcurl` in the case of Alpine Linux (musl).

## 3.18.0 (2022-01-27)

### Added

* Support for `disableClockValidation` license property.

## 3.17.2 (2021-12-08)

### Fixed

* PAC file related issue on Windows.
* False positives in VM detection for macOS.

## 3.17.1 (2021-11-30)

### Fixed

* Issue causing crash when PAC file is used for proxy settings on Windows.

## 3.17.0 (2021-11-17)

### Added

* `SetActivationLeaseDuration()`  function to allow setting lease duration from the client.

## 3.16.0 (2021-11-02)

### Added

* `GetProductVersionName()`  function to get the product version name.
* `GetProductVersionDisplayName()`  function to get the product version display name.
* `GetProductVersionFeatureFlag()`  function to get the product version feature flag.

## 3.15.4 (2021-09-30)

### Fixed

* Issue related to incorrect system encodings.

## 3.15.3 (2021-09-29)

### Fixed

* Issue causing failure in the detection of AWS EC2 VMs.

## 3.15.2 (2021-08-23)

### Fixed

* Issue causing `IsLicenseGenuine()` function to return incorrect status code in case of multi-product usage.

## 3.15.1 (2021-08-04)

### Fixed

* Issue causing crash on iOS in case of static linking.
* Issue causing crash on 32-bit Windows in case of Java.

## 3.15.0 (2021-07-14)

### Added

* Support for Android and iOS.
* Support for auto-proxy detection from PAC file on Windows.
* `SetDataDirectory()`  function to allow changing the default directory used by LexActivator to store the activation data.

## 3.14.9 (2021-05-11)

### Fixed

* Issue causing `GetActivationMeterAttributeUses()` function to return incorrect value in case `LA_IN_MEMORY` flag is used.

## 3.14.8 (2021-05-06)

### Fixed

* Issue causing networking errors on Windows.

## 3.14.7 (2021-04-22)

### Fixed

* Issue causing license callback to get invoked even after the license was deactivated.

### Updated

* Dropped dependency on `libnss3` for Linux.

## 3.14.6 (2021-03-24)

### Fixed

* Issue in offline activation when offline response file of some other machine is used for activation.

## 3.14.5 (2021-02-25)

### Fixed

* Issue causing license callback of deactivated activation to trigger in the case when license deactivation fails.

## 3.14.4 (2021-02-24)

### Fixed

* Intermittent crashes in multi-threaded usage.

## 3.14.3 (2021-02-12)

### Fixed

* Improved performance of incrementing meter attributes in `LA_IN_MEMORY` mode.

## 3.14.2 (2021-01-25)

### Fixed

* Intermittent crashes in multi-threaded usage.

## 3.14.1 (2021-01-18)

### Fixed

* Buffer overflow issues causing activation verification to fail.

## 3.14.0 (2021-01-11)

### Added

* &#x20;Support for preventing activation of license inside the container.

## 3.13.1 (2020-12-28)

### Fixed

* Intermittent crashes on high concurrent usage.

## 3.13.0 (2020-12-03)

### Updated

* Internal implementation of incrementing meter attributes resulting in increased performance and better concurrency support.

## 3.12.2 (2020-11-25)

### Fixed

* Caching issue causing IsLicenseGenuine() function to return LA\_FAIL when multiple instances of the app are run on the same machine.

## 3.12.1 (2020-10-23)

### Fixed

* Issue causing LexActivator to be flagged as a malicious file by anti-viruses on Windows.

## 3.12.0 (2020-09-16)

### Added

* Support for bypassing system proxy settings. Just add `api.cryptlex.com` to the bypass proxy hosts list in the system proxy settings.

### Updated

* `DeactivateLicense()`  function doesn't reset the license key in case of `hosted-floating` license type.

## 3.11.1 (2020-08-18)

### Fixed

* Bug causing the cache to return incorrect status code.

## 3.11.0 (2020-07-14)

### Added

* `SetCustomDeviceFingerprint()`  function to allow setting a custom device fingerprint.
* `GetLicenseAllowedActivations()`  function to get the allowed activations of the license.
* `GetLicenseTotalActivations()` function to get the total activations of the license.
* `GetLibraryVersion()` function to get the library version.

### Updated

* `GetLicenseMeterAttribute()`  function to return gross uses of the meter attribute.

### Fixed

* Bug causing fingerprint mismatch error in Dockers

## 3.10.1 (2020-06-12)

### Added

* Improved device fingerprinting of devices running Linux.

## 3.10.0 (2020-06-01)

### Added

* Improved device fingerprinting of devices running Linux.

### Fixed

* Bug preventing auto-detection of system proxy.

## 3.9.3 (2020-05-14)

### Fixed

* Bug causing crash in multi-threaded use.

## 3.9.2 (2020-04-20)

### Fixed

* Minor bug fixes.

## 3.9.1 (2020-04-14)

### Fixed

* Bug preventing the detection of Hyper-V on some Windows 10 machines.

## 3.9.0 (2020-03-28)

### Added

* LexActivator functions are now thread-safe.

### Fixed

* Minor bug fixes

## 3.8.0 (2019-11-18)

### Added

* `SetOfflineActivationRequestMeterAttributeUses()`  function to support meter attributes for offline activations.

### Fixed

* Minor bug fixes.

## 3.7.2 (2019-10-02)

### Fixed

* Minor bug fixes.

## 3.7.1 (2019-07-02)

### Fixed

* Minor bug fixes.

## 3.7.0 (2019-05-15)

### Added

* `GetActivationMeterAttributeUses()`, `IncrementActivationMeterAttributeUses()`, `DecrementActivationMeterAttributeUses()`, `ResetActivationMeterAttributeUses()` and `GetLicenseMeterAttribute()` functions to add support for meter attributes.

### Updated

* LexActivator wrappers for all the languages have been updated with above mentioned API function. Please update your wrappers using the latest code on [Github](https://github.com/cryptlex).

## 3.6.0 (2019-04-30)

### Added

* `SetLicenseUserCredential()`  function for user authentication. If `requireAuthentication` property of license is set to `true` then this function must be called before invoking `ActivateLicense()` or `IsLicenseGenuine()` function.

## 3.5.0 (2019-04-04)

### Added

* `GetLicenseUserCompany()` and `GetLicenseUserMetadata()`  functions to fetch user company and user metadata.
* `GetServerSyncGracePeriodExpiryDate()` function to get the grace period expiry date for server sync.
* `CheckForReleaseUpdate()` function to easily detect the [software updates](https://docs.cryptlex.com/release-management/distributing-releases#using-lexactivator) in your app.

## 3.4.0 (2019-03-25)

### Added

* `LA_IN_MEMORY` flag to add support for in-memory license activations, which stores license activation data in memory only instead of disk.

## 3.3.1 (2018-12-17)

### Fixed

* A bug preventing changing of permission flag from `LA_SYSTEM` to `LA_USER` when former is set first.

## 3.3.0 (2018-09-12)

### Added

* `GenerateOfflineTrialActivationRequest()` and `ActivateTrialOffline()` functions to allow for offline trial activations.

### Updated <a href="#updated" id="updated"></a>

* Wrappers for languages have been updated with `GenerateOfflineTrialActivationRequest()` and `ActivateTrialOffline()`  API functions. Please update your wrappers using the latest code on [Github](https://github.com/cryptlex).

## 3.2.0 (2018-08-20)

### Added

* `GetLicenseType()` function to get the license type (node-locked or hosted-floating).

### Updated

* Wrappers for languages have been updated with `GetLicenseType()` API function. Please update your wrappers using the latest code on [Github](https://github.com/cryptlex).

## 3.1.0 (2018-08-06)

### Added

* Support for clock offset property set for the licenses in the dashboard, which can be used to allow license and trial activations on machines where system clocks run behind the network time.

### Changed

* Time tampering detection threshold has been increased to around one hour to allow for daylight savings and minor changes in the system time.
*   On time tampering detection instead of returning `LA_E_TIME` it now returns `LA_E_TIME_MODIFIED`.&#x20;

    Now `LA_E_TIME` is returned only when the system time is behind the network time by more than the allowed clock offset.

### Updated

* Wrappers for languages have been updated with `LA_E_TIME_MODIFIED` status code. Please update your wrappers using the latest code on [Github](https://github.com/cryptlex).

## 3.0.5 (2018-07-21)

### Fixed

* A bug causing causing crash on few Windows machines, with WMIC service not running.

## 3.0.4 (2018-07-18)

### Fixed

* A bug causing causing crash on Linux, if license is deleted server side.

## 3.0.3 (2018-06-14)

### Fixed

* A bug causing insufficient system permissions error on first run on Linux.

## 3.0.2 (2018-05-30)

### Fixed

* A network SSL issue causing activations to fail for few proxies.

## 3.0.1 (2018-05-10)

### Fixed

* A network issue causing activations to fail.

## 3.0.0 (2018-05-03)

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

## 2.9.6 (2017-11-19)

### Added

* `GetProductKeyExpiryDate()` function to get the product key expiry timestamp.
* Support for Linux ARMv8 64 bit architecture

## 2.9.5 (2017-10-19)

### Fixed

* Bug preventing grace period not to expire on no server sync

## 2.9.4 (2017-09-23)

### Fixed

* Bug causing incorrect detection of Hyper-V

## 2.9.3 (2017-09-09)

### Fixed

* Bug causing grace period not to expire
* Regression causing LA\_EXPIRED to return for deactivated licenses

## 2.9.2 (2017-08-28)

### Fixed

* A major bug causing LA\_FAIL status to be returned for activated products

## 2.9.0 (2017-07-03)

### Added

* clang build for macOS

### Changed

* `ActivateProduct()` function now returns (throws) LA\_E\_ACT\_LIMIT error (exception) if activation limit is reached
* `IsProductGenuine()` function won't reactivate the product key, if deactivated server side

## 2.8.1 (2017-05-21)

### Fixed

* Embedded version

## 2.8.0 (2017-05-16)

### Added

* Support for changing product version without restart

### Fixed

* Minor bug fixes

## 2.7.1 (2017-04-05)

### Fixed

* GCE VM detection bug

## 2.7.0 (2017-03-04)

### Added

* Support for Linux ARMv5 and ARMv7 architectures
* Server sync for revoked licenses

### Fixed

* Minor bug fixes

## 2.6.1 (2017-01-26)

### Fixed

* A memory leak in `IsProductGenuine()` function if being invoked periodically

## 2.6.0 (2017-01-22)

### Changed

* `DeactivateProduct()` now returns LA\_E\_DEACT\_LIMIT instead of LA\_FAIL if deactivation limit is reached for the key

### Fixed

* Minor bug fixes

## 2.5.1 (2016-12-27)

### Changed

* All setter functions other than `SetVersionGUID()` are now only needed at the time of activation
* `DeactivateProduct()` now deactivates the product even if product key is expired

### Fixed

* AWS VM detection bug

## 2.4.0 (2016-12-12)

### Added

* `SetUserLock()` function to support user locked licenses.

### Changed

* `DeactivateProduct()` function now deactivates the product locally even if product key is already deactivated server side, and LA\_FAIL is returned.

## 2.3.0 (2016-05-22)

### Fixed

* A minor bug in offline activation.
* A minor bug in VM activation.

## 2.2.1 (2016-03-21)

### Added

* `GetExtraActivationData()` function to get the value of the extra activation data.
* `GetDaysLeftToExpiration()` function to get the number of remaining days after which the license expires.
