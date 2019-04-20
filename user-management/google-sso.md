# Google SSO

You can use Google SSO \(Single Sign On\) to reduce the number of logins required to access your web apps. Users login with their Google credentials, then access third-party applications. SSO reduces the number of passwords people need to manage.

## Enable Google SSO

In order to enable Google SSO for your account, go to the [Settings](https://app.cryptlex.com/settings) page in the Dashboard and click the **`Enable Google SSO`** button under "Use Google for Login" section.

## Enable Google SSO for sub-domain/custom domain

Your employees/team members and customers can login to the Dashboard using sub-domain or custom domain URL only. In order to enable Google SSO for sub-domain/custom domain you first need to create the Google Client Id for the sub-domain/custom domain.

### **Create the Google Client Id**

* Navigate to [Integrating Google Sign-In into your web app](https://developers.google.com/identity/sign-in/web/devconsole-project) and select **CONFIGURE A PROJECT**.
* In the Configure your OAuth client dialog, select Web browser.
* In the "Authorized Javascript Origin" text entry box, set the sub-domain/custom domain URL. For example, **https://mycompany.cryptlex.app**
* Copy the Client Id.

Then go to the [Settings](https://app.cryptlex.com/settings) page in the Dashboard and click the **`Set Google Client Id`** button and paste the Client Id.

