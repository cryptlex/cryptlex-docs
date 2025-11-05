# Using LexFloatClient with C, C++ & Objective C

First of all, login to your Cryptlex account and download the LexFloatClient library for Windows, macOS, or Linux:

* [Download LexFloatClient for Windows](https://app.cryptlex.com/developer/sdk-downloads)
* [Download LexFloatClient for macOS](https://app.cryptlex.com/developer/sdk-downloads)
* [Download LexFloatClient for Linux](https://app.cryptlex.com/developer/sdk-downloads)

The above download package contains the library (shared as well as static) which you will be using to add licensing to your app.

## Adding licensing to your app

After you've added a product for your app in the admin portal, you will need to do the following things:

* Note the product id for the product (from the actions menu in the table).
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-c).

The product id is the identifier of your product that is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding the library to your app

The LexFloatClient C example project includes the header files **LexFloatClient.h** and **LexFloatStatusCodes.h**. The **LexFloatClient.h** file defines all the LexFloatClient API functions required to add licensing to your application.

Depending on the target platform (x86, x64, or ARM64), you need to link your application with the corresponding LexFloatClient library.

{% hint style="info" %}
**LexFloatClient** requires the Microsoft Visual C++ 2015 (or later) Runtime on older Windows versions such as Windows 7, 8, or Server 2008/2012. If not already installed, install it from the official [Visual C++ Redistributable](https://www.microsoft.com/en-in/download/details.aspx?id=48145) or include the required DLLs with your installer.
{% endhint %}

### Setting product id

The first LexFloatClient API function you need to use in your code is `SetHostProductId()`. It sets the product id of the product you will be adding licensing to.&#x20;

```c
SetHostProductId("PASTE_PRODUCT_ID");
```

### Requesting floating license

To receive a floating license, you will use `SetHostUrl()`, `SetFloatingLicenseCallback()` and `RequestFloatingLicense()`LexFloatClient API methods. It sets the LexFloatServer address, the callback for status notifications, contacts the server and receives the floating license.

```c
int status;
status = SetHostProductId(L"PASTE_PRODUCT_ID");
if(LF_OK != status)
{
	// handle error
}
status = SetHostUrl("http://localhost:8090");
if(LF_OK != status)
{
	// handle error
}
status = SetFloatingLicenseCallback(LicenceRenewCallback);
if(LF_OK != status)
{
	// handle error
}
status = RequestFloatingLicense();
if(LF_OK != status)
{
	// handle error
}
printf("License leased successfully!");
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing floating license

License lease automatically renews itself in a background thread. When a license is renewed or fails to renew, the callback is invoked (from the background thread).

```c
void LF_CC LicenceRenewCallback(uint32_t status)
{
    switch (status)
	{
	case LF_OK:
		printf("The license lease has renewed successfully.\n");
		break;
	case LF_E_LICENSE_NOT_FOUND:
		printf("The license expired before it could be renewed.\n");
		break;
	case LF_E_LICENSE_EXPIRED_INET:
		printf("The license expired due to network connection failure.\n");
		break;
	default:
		printf("The license renew failed due to other reason. Error code: %d\n", status);
		break;
	}
}
```

### Dropping floating license

When your user is done using the app, the app should send a request to free the license, thereby making it available to other users. If the app doesn't, the license becomes useless (zombie) until lease time is over.

```c
int status;
status = DropFloatingLicense();
if(LF_OK != status) 
{
	// handle error
}
else 
{
    printf("Success! License dropped.");
}
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help with adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).
