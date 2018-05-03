---
description: All notable changes to LexFloatServer and LexFloatClient are documented here.
---

# LexFloatServer & Client

## 2.9.5 \(2017-10-19\)

### Fixed

* Bug preventing grace period not to expire on no server sync

## 2.9.4 \(2017-09-23\)

### Fixed

* Bug causing incorrect detection of Hyper-V

## 2.9.3 \(2017-09-09\)

### Added

* lastSyncedAt and gracePeriodStartAt properties to stats api

## 2.9.2 \(2017-08-27\)

### Fixed

* Major bug causing LA\_FAIL status to be returned for activated server

## 2.9.0 \(2017-07-03\)

### Added

* clang build for macOS

## 2.8.1 \(2017-05-21\)

### Fixed

* Embedded server version

## 2.8.0 \(2017-05-16\)

### Added

* Support for changing product version without restart

### Changed

* Disallowed leasing of licenses, if grace period is over and server is running

### Fixed

* Fixed a time sync issue

## 2.7.0 \(2017-03-04\)

### Added

* Support for running the server, in case server is not activated

### Fixed

* A startup issue as service on Windows 7

## 2.6.1 \(2017-01-26\)

### Fixed

* A memory leak issue

## 2.6.0 \(2017-01-22\)

### Added

* "status" property to the stats api

### Fixed

* Minor bug fixes

## 2.5.1 \(2016-12-27\)

### Added

* Command line parameter "-displayname" to update service name in Windows
* Command line parameter "-status" to display activation status details
* Command line parameters "-proxy", "-graceperiod", "-servercheckinterval" and "-extradata" which can only be passed at the time of activation
* Support for multiple service instances

### Removed

* Proxy, GracePeriod and ServerCheckInterval from config file

## 2.4.0 \(2016-12-12\)

### Added

* API endpoint to get the server stats: /services/api/stats
* Client IP check to prevent VM snapshot floating clients 

## 2.3.0 \(2016-05-22\)

### Added

* Support for blocking ip addresses
* Support for offline activations

