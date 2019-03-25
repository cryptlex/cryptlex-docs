---
description: All notable changes to LexFloatServer and LexFloatClient are documented here.
---

# LexFloatServer & Client

## 4.0.2 \(2019-03-25\) <a id="3-0-0-2018-05-03"></a>

### Added <a id="added-2"></a>

* **LexFloatServer:** Support for detecting Dockers to prevent running of LexFloatServer inside a Docker container. 

## 4.0.1 \(2019-02-24\) <a id="3-0-0-2018-05-03"></a>

### Added <a id="added-2"></a>

* **LexFloatServer:**  New command line parameter `-cryptlexhost` to allowing setting a custom host.

## 4.0.0 \(2018-12-17\) <a id="3-0-0-2018-05-03"></a>

### Added <a id="added-2"></a>

* **LexFloatServer:** New [/api/floating-licenses](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#getting-list-of-floating-licenses) endpoint to get the list of leased floating licenses.
* **LexFloatServer**: [Leasing strategy](https://docs.cryptlex.com/license-management/license-policies#leasing-strategy) can be set for the server to configure the behaviour of leasing floating licenses.
* **LexFloatServer**: [Lease duration](https://docs.cryptlex.com/license-management/license-policies#lease-duration) in the config can be overridden using `leaseDuration` property of license.
* **LexFloatServer:** Improved error and request logging.
* **LexFloatServer**: Server error codes like server license expired, suspended, grace period over etc. are now sent to clients too.
* **LexFloatServer**: Lot of bug fixes and core improvements.
* **LexFloatClient:** `SetFloatingClientMetadata()` and `GetHostLicenseExpiryDate()` API functions

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

