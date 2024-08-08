# LexFloatClient

## 4.9.0 (2024-08-05)

### Added

* `GetFloatingClientMetadata()` , `RequestOfflineFloatingLicense()`, `GetFloatingLicenseMode()`, `GetFloatingClientLeaseExpiryDate()`, `GetHostConfig()`, `SetPermissionFlag()`API functions.

### Updated

* `GetHostLicenseMeterAttribute()` function - Updated the data type of `allowedUses` to `int64_t`, `totalUses` to `uint64_t` and `grossUses` to `uint64_t`.

## 4.8.1 (2024-05-15)

### Updated

* Included SSL support for secure communications.

## 4.8.0 (2023-12-01)

### Added

* `GetFloatingClientLibraryVersion()` API function.

## 4.7.7 (2023-09-23)

### Fixed

* Minor bug fix.

## 4.7.6 (2023-09-21)

### Updated

* Increased default network timeout to 60 secs.

## 4.7.5 (2023-04-10)

### Fixed

* Minor bug fix.

## 4.7.4 (2022-12-05)

### Fixed

* Encoding issues in feature related functions.

## 4.7.3 (2022-10-19)

### Fixed

* Added missing digital signature for Windows DLLs.

## 4.7.2 (2022-08-10)

### Fixed

* Removed external `libcurl` dependency in Linux `musl` build.

## 4.7.1 (2022-04-12)

### Fixed

* Issue with the function name.

## 4.7.0 (2022-04-11)

### Added

* `GetHostProductVersionName()`, `GetHostProductVersionDisplayName()` and `GetHostProductVersionFeatureFlag()` API functions.

## 4.6.0 (2021-07-14)

### Added

* Support for Android and iOS.

## 4.5.3 (2021-05-06)

### Updated

* Updated networking library for Windows.

## 4.5.2 (2021-04-22)

### Updated

* Dropped dependency on `libnss3` for Linux.

## 4.5.1 (2021-04-06)

### Fixed

* Fixed a minor security issue.

## 4.5.0 (2021-03-23)

### Added

* Support for getting `grossUses` of meter attributes.

## 4.4.3 (2021-02-25)

### Fixed

* Intermittent crashes in multi-threaded usage.

## 4.3.2 (2020-01-30)

### Fixed

* Minor bug fixes.

## 4.3.1 (2019-11-19)

### Fixed

* Minor bug fixes.

## 4.1.0 (2019-07-02) <a href="#id-3-0-0-2018-05-03" id="id-3-0-0-2018-05-03"></a>

### Added <a href="#added-2" id="added-2"></a>

* `GetHostLicenseMeterAttribute()`, `GetFloatingClientMeterAttributeUses()`, `IncrementFloatingClientMeterAttributeUses()`, `DecrementFloatingClientMeterAttributeUses()` and `ResetFloatingClientMeterAttributeUses()` API functions.

## 4.0.0 (2018-12-17) <a href="#id-3-0-0-2018-05-03" id="id-3-0-0-2018-05-03"></a>

### Added <a href="#added-2" id="added-2"></a>

* `SetFloatingClientMetadata()` and `GetHostLicenseExpiryDate()` API functions.

### Changed <a href="#changed" id="changed"></a>

* All status codes have been updated.
* Header file and samples for all languages on Github have been updated.
* Renamed`GetHandle()` function to `SetHostProductId()`
* Renamed `SetFloatingServer()` function to `SetHostUrl()`
* Renamed `SetLicenseCallback()` function to `SetFloatingLicenseCallback()`
* Renamed `GetLicenseMetadata()` function to `GetHostLicenseMetadata()`
* Renamed `RequestLicense()` function to `RequestFloatingLicense()`
* Renamed `DropLicense()` function to `DropFloatingLicense()`
* Renamed `HasLicense()` function to `HasFloatingLicense()`

### Deleted <a href="#deleted" id="deleted"></a>

* `FindHandle()` function
* `GlobalCleanup()` function

## 3.0.0 (2018-05-03)

### Changed

* All status codes have been updated
* Renamed`SetVersionGUID` function to `SetProductId()`
* Renamed`GetCustomField()` function to `GetLicenseMetadata()`

### Deleted

* `SetProductFile()` function&#x20;

## 2.9.0 (2017-07-03)

### Added

* clang build for macOS
