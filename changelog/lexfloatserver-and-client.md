---
description: All notable changes to LexFloatServer and LexFloatClient are documented here.
---

# LexFloatServer & Client

## 4.4.3 \(2021-02-25\)

### Fixed

* **LexFloatServer:** Some performance-related issues.
* **LexFloatClient:** Intermittent crashes in multi-threaded usage.

## 4.4.2 \(2021-02-08\)

### Fixed

* **LexFloatServer:** Issue causing offline activation to fail when the number of meter attributes is very large.

## 4.4.1 \(2021-01-18\)

### Fixed

* **LexFloatServer:** Buffer overflow issues causing activation verification to fail.

## 4.4.0 \(2021-01-11\)

### Added

* **LexFloatServer:** Support for running the server inside a container for testing purposes. The server must never be allowed to be run inside a container. 

## 4.3.10 \(2020-09-16\)

### Added

* **LexFloatServer:** Support for bypassing system proxy settings. Just add `api.cryptlex.com` to the bypass proxy hosts list in the system proxy settings.

## 4.3.8 \(2020-08-18\)

### Fixed

* **LexFloatServer:** Bug causing the cache to return incorrect status code.

## 4.3.7 \(2020-06-12\)

### Fixed

* **LexFloatServer:** Minor bug fixes.

## 4.3.6 \(2020-06-01\)

### Added

* **LexFloatServer:**  Improved device fingerprinting of devices running Linux.

## 4.3.5 \(2020-04-14\)

### Fixed

* **LexFloatServer:** Bug preventing the detection of Hyper-V on some Windows 10 machines.

## 4.3.4 \(2020-03-20\)

### Fixed

* **LexFloatServer:** Minor bug fixes.

## 4.3.3 \(2020-03-12\)

### Fixed

* **LexFloatServer:** Minor bug fixes.

## 4.3.2 \(2020-01-30\)

### Fixed

* **LexFloatClient:** Minor bug fixes.

## 4.3.1 \(2019-11-19\)

### Fixed

* **LexFloatClient:** Minor bug fixes.

## 4.3.0 \(2019-10-28\) <a id="3-0-0-2018-05-03"></a>

### Added <a id="added-2"></a>

* **LexFloatServer:** `dailylogrotation` config file param.
* **LexFloatServer:** New [/api/server/activate](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#online-activation-1), [/api/server/offline-activation-request](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#offline-activation-1) and [/api/server/offline-activate](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#offline-activation-1) endpoints.

## 4.2.0 \(2019-07-23\) <a id="3-0-0-2018-05-03"></a>

### Added <a id="added-2"></a>

* **LexFloatServer:** `allowedclockoffset` config file param.

## 4.1.0 \(2019-07-02\) <a id="3-0-0-2018-05-03"></a>

### Added <a id="added-2"></a>

* **LexFloatServer:** Support for meter attributes.
* **LexFloatClient:** `GetHostLicenseMeterAttribute()`, `GetFloatingClientMeterAttributeUses()`, `IncrementFloatingClientMeterAttributeUses()`, `DecrementFloatingClientMeterAttributeUses()` and `ResetFloatingClientMeterAttributeUses()` API functions.

## 4.0.2 \(2019-03-25\) <a id="3-0-0-2018-05-03"></a>

### Added <a id="added-2"></a>

* **LexFloatServer:** Support for detecting Dockers to prevent running of LexFloatServer inside a Docker container. 

## 4.0.1 \(2019-02-24\) <a id="3-0-0-2018-05-03"></a>

### Added <a id="added-2"></a>

* **LexFloatServer:**  New command line parameter `-cryptlexhost` to allow setting a custom host.

## 4.0.0 \(2018-12-17\) <a id="3-0-0-2018-05-03"></a>

### Added <a id="added-2"></a>

* **LexFloatServer:** New [/api/floating-licenses](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#getting-list-of-floating-licenses) endpoint to get the list of leased floating licenses.
* **LexFloatServer**: [Leasing strategy](https://docs.cryptlex.com/license-management/license-policies#leasing-strategy) can be set for the server to configure the behaviour of leasing floating licenses.
* **LexFloatServer**: [Lease duration](https://docs.cryptlex.com/license-management/license-policies#lease-duration) in the config can be overridden using `leaseDuration` property of license.
* **LexFloatServer:** Improved error and request logging.
* **LexFloatServer**: Server error codes like server license expired, suspended, grace period over etc. are now sent to clients too.
* **LexFloatServer**: Lot of bug fixes and core improvements.
* **LexFloatClient:** `SetFloatingClientMetadata()` and `GetHostLicenseExpiryDate()` API functions.

### Changed <a id="changed"></a>

* **LexFloatServer:** Updated stats API endpoint, for details check [docs](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#getting-server-stats)​
* **LexFloatServer:** Minimum supported LexFloatClient version is `v4.0.0.`
* **LexFloatClient:** All status codes have been updated.
* **LexFloatClient**: Header file and samples for all languages on Github have been updated.
* **LexFloatClient:** Renamed`GetHandle()` function to `SetHostProductId()`
* **LexFloatClient:** Renamed `SetFloatingServer()` function to `SetHostUrl()`
* **LexFloatClient:** Renamed `SetLicenseCallback()` function to `SetFloatingLicenseCallback()`
* **LexFloatClient:** Renamed `GetLicenseMetadata()` function to `GetHostLicenseMetadata()`
* **LexFloatClient:** Renamed `RequestLicense()` function to `RequestFloatingLicense()`
* **LexFloatClient:** Renamed `DropLicense()` function to `DropFloatingLicense()`
* **LexFloatClient:** Renamed `HasLicense()` function to `HasFloatingLicense()`

### Deleted <a id="deleted"></a>

* **LexFloatClient:** `FindHandle()` function
* **LexFloatClient:** `GlobalCleanup()` function

## 3.0.2 \(2018-09-10\)

### Added

* **LexFloatServer:** Added activation and deactivation logs to the log file.

## 3.0.1 \(2018-08-20\)

### Added

* **LexFloatServer:** Fixed a bug preventing server from running as launchd daemon on MacOS.

## 3.0.0 \(2018-05-03\)

### Added

* **LexFloatServer:** Command line parameters `-metadatakey` & `-metadatavalue`

### Changed

* **LexFloatClient:** All status codes have been updated
* **LexFloatClient:** Renamed`SetVersionGUID` function to `SetProductId()`
* **LexFloatClient:** Renamed`GetCustomField()` function to `GetLicenseMetadata()`
* **LexFloatServer:** Updated stats API endpoint, for details check [docs](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#getting-server-stats)
* **LexFloatServer:** Now uses `LexActivator` `v3.0.0` for license activation
* **LexFloatServer:** Renamed command line parameter `-pkey` to `-licensekey`
* **LexFloatServer:** Renamed command line parameter `-pfile` to `-productfile`
* **LexFloatServer:** Renamed command line parameter `-orequest` to `-offlinerequest`
* **LexFloatServer:** Renamed command line parameter `-oresponse` to `-offlineresponse`

### Deleted

* **LexFloatClient:** `SetProductFile()` function
* **LexFloatServer:** Command line parameter `-extradata` 

## 2.9.5 \(2017-10-19\)

### Fixed

* **LexFloatServer:** Bug preventing grace period not to expire on no server sync

## 2.9.4 \(2017-09-23\)

### Fixed

* **LexFloatServer:** Bug causing incorrect detection of Hyper-V

## 2.9.3 \(2017-09-09\)

### Added

* **LexFloatServer:** `lastSyncedAt` and `gracePeriodStartAt` properties to stats API

## 2.9.2 \(2017-08-27\)

### Fixed

* **LexFloatServer:** Major bug causing `LA_FAIL` status to be returned for activated server

## 2.9.0 \(2017-07-03\)

### Added

* **LexFloatClient:** clang build for macOS

## 2.8.1 \(2017-05-21\)

### Fixed

* **LexFloatServer:** Embedded server version

## 2.8.0 \(2017-05-16\)

### Added

* **LexFloatServer:** Support for changing product version without restart

### Changed

* **LexFloatServer:** Disallowed leasing of licenses, if grace period is over and server is running

### Fixed

* **LexFloatServer:** Fixed a time sync issue

## 2.7.0 \(2017-03-04\)

### Added

* **LexFloatServer:** Support for running the server, in case server is not activated

### Fixed

* **LexFloatServer:** A startup issue as service on Windows 7

## 2.6.1 \(2017-01-26\)

### Fixed

* **LexFloatServer:** A memory leak issue

## 2.6.0 \(2017-01-22\)

### Added

* **LexFloatServer:** `status` property to the stats api

### Fixed

* **LexFloatServer:** Minor bug fixes

## 2.5.1 \(2016-12-27\)

### Added

* **LexFloatServer:** Command line parameter `-displayname` to update service name in Windows
* **LexFloatServer:** Command line parameter `-status` to display activation status details
* **LexFloatServer:** Command line parameters `-proxy`, `-graceperiod`, `-servercheckinterval` and `-extradata` which can only be passed at the time of activation
* **LexFloatServer:** Support for multiple service instances

### Removed

* **LexFloatServer:** `Proxy`, `GracePeriod` and `ServerCheckInterval` from config file

## 2.4.0 \(2016-12-12\)

### Added

* **LexFloatServer:** API endpoint to get the server stats: /services/api/stats
* **LexFloatServer:** Client IP check to prevent VM snapshot floating clients 

## 2.3.0 \(2016-05-22\)

### Added

* **LexFloatServer:** Support for blocking ip addresses
* **LexFloatServer:** Support for offline activations

