# Google SSO

You can use Google SSO (Single Sign On) to reduce the number of logins required to access your web apps. Users login with their Google credentials, then access third-party applications. SSO reduces the number of passwords people need to manage.

## Enable Google SSO

To enable Google SSO for your account, go to the `Settings -> Profile page` in the admin portal and click the **`Enable Google Login`** button.

## Enable Google SSO for sub-domain/custom domain

Your customers and resellers can log in to the customer and reseller portals using Cryptlx sub-domain or custom domain URLs only. To enable Google SSO for sub-domain/custom domain you first need to create the Google Client ID for the sub-domain/custom domain.

### **Create the Google Client ID**

* Navigate to [Integrating Google Sign-In into your web app](https://developers.google.com/identity/sign-in/web/devconsole-project) and select **CONFIGURE A PROJECT**.
* In the Configure your OAuth client dialog, select Web browser.
* In the "Authorized Javascript Origin" text entry box, set the sub-domain/custom domain URLs. For example, https://mycompany.customer.cryptlex.com, https://mycompany.reseller.cryptlex.com etc.
* Copy the Client ID.

Then go to the `Settings -> Account` page in the admin portal and click the **`Configure Google SSO`** button and paste the Client ID.
