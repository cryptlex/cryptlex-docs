# SAML SSO

Single sign-on \(SSO\) allows users of your Cryptlex account to log in using your existing SAML-enabled identity provider, such as Active Directory, OneLogin, Auth0, Okta, and many more. This reduces the number of passwords your users need to manage. It also makes provisioning new users a breeze.

## Configuring single sign-on with SAML <a id="h_89fbe606-11a7-44be-9a19-35a2bd1017a5"></a>

To get started, go to **Settings &gt; Security** in the Dashboard and click the **`Enable SAML SSO`** button. This will display the SAML SSO settings dialog where you can add details of your identity provider.

Cryptlex supports the SAML 2.0 standard, which provides a few ways to streamline configuration. Although each identity provider will have different interfaces and nuances, most provide configuration metadata as a URL. Since each identity provider is unique, we will only cover using Cryptlex with a generic SAML identity provider in this article.

The easiest way to configure SSO is to use a link to your identity provider's metadata file. Simply enter the URL in the **SAML IdP** **Metadata URL** input box and click **Save**. Cryptlex will download the configuration file, parse it, and configure everything.

## Auto-Provisioning users <a id="h_b3fa72f1-91b7-4c82-b174-fbe0427876c5"></a>

The SAML identity provider must be configured to provide four attributes: **Email**, **FirstName**, **LastName,** and **Role**. These attributes allow Cryptlex to properly identify the user and automatically provision users.

{% hint style="info" %}
**FirstName**, **LastName,** and **Role** are only required if the auto-provisioning of users is enabled.
{% endhint %}

### Email

Every user in your Cryptlex account is required to have a valid email address, even when using SSO. Since the identity provider is responsible for managing user information, it must send the user's email address to Cryptlex in its assertion. Identity providers use different naming conventions, so Cryptlex will look for an email address in the following attributes \(case-insensitive\) sequentially:

* [http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress)
* EmailAddress
* Email
* Mail
* User.email
* http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name

### FirstName

Just like email addresses, identity providers may send the first name in several common fields. To provide out-of-the-box compatibility with most identity providers, Cryptlex will try to find the first name in the following attributes \(case-insensitive\):

* [http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname)
* FirstName
* first\_name
* User.FirstName

### LastName

Cryptlex looks for the last name in the following attributes \(case-insensitive\):

* [http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname)
* LastName
* last\_name
* User.LastName

### Role

If your identity provider supports custom attributes, you can set the Role attribute to automatically provision users with roles created in Cryptlex This can be set to any valid role on your Cryptlex account. Cryptlex looks for the role in the following attributes \(case-insensitive\):

* [http://schemas.microsoft.com/ws/2008/06/identity/claims/role](http://schemas.microsoft.com/ws/2008/06/identity/claims/role)
* Role

#### Role mapping

You can easily map the roles created in Cryptlex \(service provider roles\) with your existing roles in the identity provider. Then depending on the identity provider role in the SAML assertion, Cryptlex will use the corresponding service provider role when auto-provisioning the user.  

