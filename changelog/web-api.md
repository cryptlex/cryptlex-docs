---
description: All notable changes to Web API are documented here.
---

# Web API

## 3.0.2 \(2018-05-19\)

### Added {#changed}

* `licensePolicyId` property to licenses to override the default license policy inherited through product.

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

