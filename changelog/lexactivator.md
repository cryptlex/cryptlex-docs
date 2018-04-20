---
description: All notable changes to LexActivator are documented here.
---

# LexActivator

## [2.9.6] - 2017-11-19
### Added
- GetProductKeyExpiryDate() function to get the product key expiry timestamp.
- Support for Linux ARMv8 64 bit architecture

## [2.9.5] - 2017-10-19
### Fixed
- Bug preventing grace period not to expire on no server sync

## [2.9.4] - 2017-09-23
### Fixed
- Bug causing incorrect detection of Hyper-V

## [2.9.3] - 2017-09-09
### Fixed
- Bug causing grace period not to expire
- Regression causing LA_EXPIRED to return for deactivated licenses

## [2.9.2] - 2017-08-28
### Fixed
- A major bug causing LA_FAIL status to be returned for activated products

## [2.9.0] - 2017-07-03
### Added
- clang build for macOS

### Changed
- ActivateProduct() function now returns (throws) LA_E_ACT_LIMIT error (exception) if activation limit is reached
- IsProductGenuine() function won't reactivate the product key, if deactivated server side


## [2.8.1] - 2017-05-21
### Fixed
- Embedded version

## [2.8.0] - 2017-05-16
### Added
- Support for changing product version without restart

### Fixed
- Minor bug fixes

## [2.7.1] - 2017-04-05
### Fixed
- GCE VM detection bug

## [2.7.0] - 2017-03-04
### Added
- Support for Linux ARMv5 and ARMv7 architectures
- Server sync for revoked licenses

### Fixed
- Minor bug fixes

## [2.6.1] - 2017-01-26
### Fixed
- A memory leak in IsProductGenuine() function if being invoked periodically

## [2.6.0] - 2017-01-22
### Changed
- DeactivateProduct() now returns LA_E_DEACT_LIMIT instead of LA_FAIL if deactivation limit is reached for the key

### Fixed
- Minor bug fixes

## [2.5.1] - 2016-12-27
### Changed
- All setter functions other than SetVersionGUID() are now only needed at the time of activation
- DeactivateProduct() now deactivates the product even if product key is expired

### Fixed
- AWS VM detection bug

## [2.4.0] - 2016-12-12
### Added
- SetUserLock() function to support user locked licenses.

### Changed
- DeactivateProduct() function now deactivates the product locally even if product key is already deactivated server side, and LA_FAIL is returned.

## [2.3.0] - 2016-05-22
### Fixed
- A minor bug in offline activation.
- A minor bug in VM activation.

## [2.2.1] - 2016-03-21
### Added
- GetExtraActivationData() function to get the value of the extra activation data.
- GetDaysLeftToExpiration() function to get the number of remaining days after which the license expires.
