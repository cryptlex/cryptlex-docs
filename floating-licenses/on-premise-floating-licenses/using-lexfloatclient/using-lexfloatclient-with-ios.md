# Using LexFloatClient with iOS

First of all, login to your Cryptlex account and download the LexActivator library for iOS:

* [Download LexFloatClient for iOS](https://app.cryptlex.com/downloads)

The above download package contains the library in the .xcframework format. The .xcframework supports the following architectures:

* iOS Simulator - x86\_64 \(Intel\), ARM64 \(Apple Silicon\) 
* iOS - ARM64

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-ios/tree/main/examples/sample).

The product id is the identifier of your product that is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding the library to your app

After downloading the library in .xcframework format, just add it to your project in Xcode. You can add the dynamic as well as the static framework depending on your requirements.   

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

