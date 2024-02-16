# LexFloatServer

## 4.11.2 (2023-12-22)

### Fixed

* Minor bug fixes.

## 4.11.1 (2023-12-14)

### Updated

* LexActivator version to v3.25.0

## 4.11.0 (2023-12-07)

### Added

* `enableIpv6` config file param to enable LexFloatServer to serve requests over IPv6.

### Fixed

* `productFilePath` config file param now takes an absolute path as well.

## 4.10.0 (2023-11-09)

### Added

* `/api/server/license-meter-attributes` endpoint to get the meter attributes associated with the license.

### Updated

* Improved meter attribute logs.

### Fixed

* Minor bug fixes.

## 4.9.5 (2023-09-21)

### Updated

* LexActivator version to v3.24.1

## 4.9.4 (2023-08-11)

### Fixed

* Added missing WMI service error log.
* Enforced service startup type to auto-delayed (Windows).

### Updated

* LexActivator version to v3.23.0

## 4.9.3 (2023-06-24)

### Fixed

* Minor bug fix.

## 4.9.2 (2023-06-03)

### Fixed

* Issues related to service uninstallation on Windows.

### Updated

* LexActivator version to v3.21.4.

## 4.9.1 (2023-05-05)

### Fixed

* Minor bug fixes.

## 4.9.0 (2023-04-04)

### Added

* `/api/server/license-info` endpoint to get the information related to the license used to activate the LexFloatServer.

### Fixed

* Issue related to the service path on Linux.

## 4.8.10 (2023-02-10)

### Fixed

* False positive container detection on some Linux distributions.

## 4.8.9 (2023-02-10)

### Fixed

* Container detection issue on recent Linux distributions.

## 4.8.8 (2022-12-01)

### Updated

* LexActivator version to v3.20.7.

## 4.8.7 (2022-11-03)

### Updated

* LexActivator version to v3.20.2.

## 4.8.6 (2022-10-31)

### Fixed

* Added missing digital signature in case of Windows.

## 4.8.5 (2022-07-26)

### Updated

* Improved error logs.

## 4.8.4 (2022-07-05)

### Updated

* Allow activation if the server is already activated.

## 4.8.3 (2022-07-01)

### Fixed

* Added missing error return codes.

## 4.8.2 (2022-06-20)

### Updated

* LexActivator version to v3.19.1.

## 4.8.1 (2022-06-15)

### Updated

* Support for the new product.dat file.

## 4.8.0 (2022-04-06)

### Added

* Support for the feature flags.

## 4.7.0 (2021-12-08)

### Updated

* Improved logging.

### Fixed

* Issues related to meter attributes when the license is activated through Dashboard.

## 4.6.8 (2021-08-11)

### Fixed

* Incorrect exit return codes.

## 4.6.7 (2021-08-11)

### Fixed

* Minor bug fixes.

## 4.6.6 (2021-08-03)

### Fixed

* Minor bug fixes.

## 4.6.5 (2021-07-15)

### Updated

* Minor performance improvements.

## 4.6.4 (2021-07-08)

### Fixed

* Issue related to log folder path.

## 4.6.3 (2021-06-15)

### Fixed

* Issues related to incrementing of meter attributes.
* Issue related to incorrect encoding.

## 4.6.2 (2021-06-15)

### Fixed

* Issue causing server activation to disappear on restart in Windows.

## 4.6.1 (2021-06-15)

### Fixed

* Minor bug fixes.

## 4.6.0 (2021-06-14) <a href="#id-3-0-0-2018-05-03" id="id-3-0-0-2018-05-03"></a>

### Added <a href="#added-2" id="added-2"></a>

* Multi-threading support so it can now be vertically scaled to handle thousands of clients.
* Dashboard wherein you can login, view active floating licenses, activate/deactivate the LexFloatServer etc.
* Improved logging and colored console logs are supported too on Linux and macOS.
* Supports for running as service on Linux without writing any systemd or init script.

### Changed <a href="#changed" id="changed"></a>

* Command-line options are now posix-compliant. Please check the updated options using lexfloatserver --help command.
* YAML based config file and by default lexfloatserver looks for config.yml file in the same directory as lexfloatserver, so you don't need to pass the config file path.

## 4.5.3 (2021-05-06)

### Updated

* Updated networking library for Windows.

## 4.5.2 (2021-04-22)

### Updated

* Dropped dependency on `libnss3` for Linux.

## 4.5.1 (2021-04-06)

### Fixed

* Minor bug fix.

## 4.5.0 (2021-03-23)

### Added

* Support for persistent meter attributes (non-floating).&#x20;
* Support for offline syncing of meter attributes (non-floating) during offline activation.

## 4.4.3 (2021-02-25)

### Fixed

* Some performance-related issues.

## 4.4.2 (2021-02-08)

### Fixed

* Issue causing offline activation to fail when the number of meter attributes is very large.

## 4.4.1 (2021-01-18)

### Fixed

* Buffer overflow issues causing activation verification to fail.

## 4.4.0 (2021-01-11)

### Added

* Support for running the server inside a container for testing purposes. The server must never be allowed to be run inside a container.&#x20;

## 4.3.10 (2020-09-16)

### Added

* Support for bypassing system proxy settings. Just add `api.cryptlex.com` to the bypass proxy hosts list in the system proxy settings.

## 4.3.8 (2020-08-18)

### Fixed

* Bug causing the cache to return incorrect status code.

## 4.3.7 (2020-06-12)

### Fixed

* Minor bug fixes.

## 4.3.6 (2020-06-01)

### Added

* Improved device fingerprinting of devices running Linux.

## 4.3.5 (2020-04-14)

### Fixed

* Bug preventing the detection of Hyper-V on some Windows 10 machines.

## 4.3.4 (2020-03-20)

### Fixed

* Minor bug fixes.

## 4.3.3 (2020-03-12)

### Fixed

* Minor bug fixes.

## 4.3.0 (2019-10-28) <a href="#id-3-0-0-2018-05-03" id="id-3-0-0-2018-05-03"></a>

### Added <a href="#added-2" id="added-2"></a>

* `dailylogrotation` config file param.
* New [/api/server/activate](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#online-activation-1), [/api/server/offline-activation-request](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#offline-activation-1) and [/api/server/offline-activate](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#offline-activation-1) endpoints.

## 4.2.0 (2019-07-23) <a href="#id-3-0-0-2018-05-03" id="id-3-0-0-2018-05-03"></a>

### Added <a href="#added-2" id="added-2"></a>

* `allowedclockoffset` config file param.

## 4.1.0 (2019-07-02) <a href="#id-3-0-0-2018-05-03" id="id-3-0-0-2018-05-03"></a>

### Added <a href="#added-2" id="added-2"></a>

* Support for meter attributes.

## 4.0.2 (2019-03-25) <a href="#id-3-0-0-2018-05-03" id="id-3-0-0-2018-05-03"></a>

### Added <a href="#added-2" id="added-2"></a>

* Support for detecting Dockers to prevent the running of LexFloatServer inside a Docker container.&#x20;

## 4.0.1 (2019-02-24) <a href="#id-3-0-0-2018-05-03" id="id-3-0-0-2018-05-03"></a>

### Added <a href="#added-2" id="added-2"></a>

* New command line parameter `-cryptlexhost` to allow setting a custom host.

## 4.0.0 (2018-12-17) <a href="#id-3-0-0-2018-05-03" id="id-3-0-0-2018-05-03"></a>

### Added <a href="#added-2" id="added-2"></a>

* New [/api/floating-licenses](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#getting-list-of-floating-licenses) endpoint to get the list of leased floating licenses.
* [Leasing strategy](https://docs.cryptlex.com/license-management/license-policies#leasing-strategy) can be set for the server to configure the behaviour of leasing floating licenses.
* [Lease duration](https://docs.cryptlex.com/license-management/license-policies#lease-duration) in the config can be overridden using `leaseDuration` property of license.
* Improved error and request logging.
* Server error codes like server license expired, suspended, grace period over etc. are now sent to clients too.
* `SetFloatingClientMetadata()` and `GetHostLicenseExpiryDate()` API functions.

### Changed <a href="#changed" id="changed"></a>

* Updated stats API endpoint, for details, check [docs](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#getting-server-stats)​
* The Minimum supported LexFloatClient version is `v4.0.0`

## 3.0.2 (2018-09-10)

### Added

* Added activation and deactivation logs to the log file.

## 3.0.1 (2018-08-20)

### Added

* Fixed a bug preventing server from running as launchd daemon on MacOS.

## 3.0.0 (2018-05-03)

### Added

* Command-line parameters `-metadatakey` & `-metadatavalue`

### Changed

* Updated stats API endpoint, for details, check [docs](https://docs.cryptlex.com/floating-licenses/on-premise-floating-licenses/lexfloatserver#getting-server-stats)
* Now uses `LexActivator` `v3.0.0` for license activation
* Renamed command line parameter `-pkey` to `-licensekey`
* Renamed command line parameter `-pfile` to `-productfile`
* Renamed command line parameter `-orequest` to `-offlinerequest`
* Renamed command line parameter `-oresponse` to `-offlineresponse`

### Deleted

* Command-line parameter `-extradata`&#x20;

## 2.9.5 (2017-10-19)

### Fixed

* Bug preventing grace period not to expire on no server sync

## 2.9.4 (2017-09-23)

### Fixed

* Bug causing incorrect detection of Hyper-V

## 2.9.3 (2017-09-09)

### Added

* `lastSyncedAt` and `gracePeriodStartAt` properties to stats API

## 2.9.2 (2017-08-27)

### Fixed

* Major bug causing `LA_FAIL` status to be returned for activated server

## 2.8.1 (2017-05-21)

### Fixed

* Embedded server version

## 2.8.0 (2017-05-16)

### Added

* Support for changing product version without restart

### Changed

* Disallowed leasing of licenses, if grace period is over and server is running

### Fixed

* Fixed a time sync issue

## 2.7.0 (2017-03-04)

### Added

* Support for running the server, in case server is not activated

### Fixed

* A startup issue as service on Windows 7

## 2.6.1 (2017-01-26)

### Fixed

* A memory leak issue

## 2.6.0 (2017-01-22)

### Added

* `status` property to the stats api

### Fixed

* Minor bug fixes

## 2.5.1 (2016-12-27)

### Added

* Command-line parameter `-displayname` to update service name in Windows
* Command-line parameter `-status` to display activation status details
* Command-line parameters `-proxy`, `-graceperiod`, `-servercheckinterval` and `-extradata` which can only be passed at the time of activation
* Support for multiple service instances

### Removed

* `Proxy`, `GracePeriod` and `ServerCheckInterval` from config file

## 2.4.0 (2016-12-12)

### Added

* API endpoint to get the server stats: /services/api/stats
* Client IP check to prevent VM snapshot floating clients&#x20;

## 2.3.0 (2016-05-22)

### Added

* Support for blocking IP addresses
* Support for offline activations
