# Using LexFloatClient with C, C++ & Objective C

First of all, login to your Cryptlex account and download LexFloatClient library for Windows, MacOS or Linux:

* [Download LexFloatClient for Windows](https://app.cryptlex.com/downloads)
* [Download LexFloatClient for MacOS](https://app.cryptlex.com/downloads)
* [Download LexFloatClient for Linux](https://app.cryptlex.com/downloads)

The above download package contains the library \(shared as well as static\) which you will be using to add licensing to your app.

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-c).

Product id is the identifier of your product which is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding library to your app

LexFloatClient example project for C contains the **LexFloatClient.h** header file. In addition to that it includes **LexFloatClient.lib** file required in case of Windows. It contains all the LexFloatClient API functions needed to add licensing to your app.

Depending on the platform you are targeting **\(x86 or x64\)** you need to link the respective LexFloatClient.dll with your application.

### Setting product id

The first LexFloatClient API function you need to use in your code is `GetHandle()`. It sets the product id of the product you will be adding licensing to. 

```c
unsigned int handle;
GetHandle("PASTE_PRODUCT_ID", &handle);
```

### Requesting license lease

To receive a floating license, you will use `SetFloatServer()`, `SetLicenseCallback()` and `RequestLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for status notifications, contacts the server and receives the leased license.

```c
int status;
unsigned int handle;
status = GetHandle(L"YOUR VERSION GUID", &handle);
if(LF_OK != status)
{
	// handle error
}
status = SetFloatServer(handle, "localhost",8090);
if(LF_OK != status)
{
	// handle error
}
status = SetLicenseCallback(handle, LicenceRefreshCallback);
if(LF_OK != status)
{
	// handle error
}
status = RequestLicense(handle);
if(LF_OK != status)
{
	// handle error
}
printf("License leased successfully!");
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing license lease

License lease automatically renews itself in a background thread. When something goes wrong, Callback is invoked \(from background thread\).

```c
void LF_CC LicenceRefreshCallback(uint32_t status)
{
    switch (status)
    {
		case LF_E_LICENSE_EXPIRED:
			printf("The lease expired before it could be renewed.\n");
			break;
		case LF_E_LICENSE_EXPIRED_INET:
			printf("The lease expired due to network connection failure.\n");
			break;
		case LF_E_SERVER_TIME:
			printf("The lease expired because Server System time was modified.\n");
			break;
		case LF_E_TIME:
			printf("The lease expired because Client System time was modified.\n");
			break;
		default:
		    printf("The lease expired due to some other reason.\n");
			break;
    }
}
```

You would usually request for a new license if Callback gets invoked.

### Dropping license lease

When your user is done using the app, the app should send a request to free the license, thereby making it available for other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```c
int status;
status = DropLicense(handle);
if(LF_OK != status) 
{
	// handle error
}
else 
{
    printf("Success! License dropped.");
}
GlobalCleanUp();
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

