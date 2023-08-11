---
description: License Activation
---

# Named User Licenses

The license activation process encompasses two distinct methods, each serving to activate the software license. The first method involves users inputting the designated license key through an interface seamlessly integrated into the application. The alternative approach, on the other hand, asks users to enter their specific credentials to initiate license activation. This document provides a comprehensive elucidation of the latter approach:

#### Authenticating the user

User authentication is achieved through the utilization of the `AuthenticateUser()` LexActivator API function, which internally interfaces with the `/v3/accounts/login` endpoint.&#x20;

In scenarios where users have opted for Two-Factor Authentication (TFA), executing this function results in an `LA_E_TWO_FACTOR_AUTHENTICATION_CODE_MISSING` exception. In such instances, it becomes necessary to provide the TFA code using the `SetTwoFactorAuthenticationCode()` LexActivator API function. Once the code has been set successfully reinvoking the `AuthenticateUser()` LexActivator API function is required.

#### Retrieving the user License

Upon successful user authentication, `GetUserLicenses()` LexActivator API function can be invoked to retrieve licenses associated with the user. The acquired license key can then be channeled to the `SetLicenseKey()` LexActivator API function for further processing. In scenarios where multiple licenses are linked to a particular user, it is possible to prompt the user's selection of any license for activation purposes.
