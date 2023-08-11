# Named User Licenses

A named user license is a licensing model in which the software or service is allocated to a specific individual, typically identified by a unique email address.&#x20;

This model necessitates license activation using the designated user's credentials, moving away from the traditional use of license keys.&#x20;

Named user licenses can be either node-locked or floating. Regardless of the type, users must authenticate to access the licenses associated with their account. The typical process involves the following three steps:

## 1- Authenticating the user

User authentication is achieved by calling the `AuthenticateUser(string email, string password)` LexActivator API function.

In scenarios where users have enabled two-factor authentication (2FA), executing the function results in a `LA_E_TWO_FACTOR_AUTHENTICATION_CODE_MISSING` exception. In such instances, it becomes necessary to provide the 2FA code using the `SetTwoFactorAuthenticationCode()` LexActivator API function.

Once the 2FA code has been set, you need to call the `AuthenticateUser()` LexActivator API function again.

## 2- Retrieving the user license

Upon successful user authentication, `GetUserLicenses()` LexActivator API function can be used to retrieve licenses associated with the user. The acquired license key can then be passed to the `SetLicenseKey()` LexActivator API function for further processing. \
\
In scenarios where multiple licenses are linked to a particular user, it is possible to prompt the user's selection of any license for activation purposes.

## 3- Activating the license

Once the license key is obtained, the subsequent activation procedure aligns closely with the guidelines provided in the documentation for each respective [programming language](node-locked-licenses/using-lexactivator/). To activate the license within your application, simply call the `ActivateLicense()` function from the LexActivator API.
