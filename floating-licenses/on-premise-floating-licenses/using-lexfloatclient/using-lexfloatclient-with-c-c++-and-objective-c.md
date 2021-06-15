# Using LexFloatClient with C, C++ & Objective C

First of all, login to your Cryptlex account and download the LexFloatClient library for Windows, macOS, or Linux:

* [Download LexFloatClient for Windows](https://app.cryptlex.com/downloads)
* [Download LexFloatClient for macOS](https://app.cryptlex.com/downloads)
* [Download LexFloatClient for Linux](https://app.cryptlex.com/downloads)

The above download package contains the library \(shared as well as static\) which you will be using to add licensing to your app.

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-c).

The product id is the identifier of your product that is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding the library to your app

LexFloatClient example project for C contains the **LexFloatClient.h** header file. In addition to that, it includes the **LexFloatClient.lib** file required in the case of Windows. It contains all the LexFloatClient API functions needed to add licensing to your app.

Depending on the platform you are targeting **\(x86 or x64\)** you need to link the respective LexFloatClient.dll with your application.

LexFloatClient has a dependency on `VS2015` runtime on **Windows**. On the target machines where you will deploy your app, you can install the `VS2015` runtime, if not present, using the link: [https://www.microsoft.com/en-in/download/details.aspx?id=48145](https://www.microsoft.com/en-in/download/details.aspx?id=48145)

### Setting product id

The first LexFloatClient API function you need to use in your code is `SetHostProductId()`. It sets the product id of the product you will be adding licensing to. 

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

License lease automatically renews itself in a background thread. When a license is renewed or fails to renew, the callback is invoked \(from the background thread\).

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

When your user is done using the app, the app should send a request to free the license, thereby making it available to other users. If the app doesn't, the license becomes useless \(zombie\) until lease time is over.

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

