# Using LexActivator with C, C++ and Objective C

First of all, login to your Cryptlex account and download the LexActivator library for Windows, macOS or Linux:

* [Download LexActivator for Windows](https://app.cryptlex.com/developer/sdk-downloads)
* [Download LexActivator for macOS](https://app.cryptlex.com/developer/sdk-downloads)
* [Download LexActivator for Linux](https://app.cryptlex.com/developer/sdk-downloads)

The above download package contains the library (shared as well as static) which you will be using to add licensing to your app.

## Adding licensing to your app

After you've added a product for your app in the admin portal, you will need to do the following things:

* Note the product id for the product (from the actions menu in the table).
* Download the Product.dat for the product (from the actions menu in the table).
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-c).

Product.dat contains product data that is used by LexActivator. The product id is the identifier of your product that is to be used in the code.

### Adding the library to your app

The LexActivator C example project includes the header files **LexActivator.h**, **LexStatusCodes.h**, and **LexTypes.h**. The **LexActivator.h** file defines all the LexActivator API functions required to add licensing to your application.

Depending on the target platform x86, x64, or ARM64 you need to link your application with the corresponding LexActivator library.

{% hint style="info" %}
**LexActivator** requires the Microsoft Visual C++ 2015 (or later) Runtime on older Windows versions such as Windows 7, 8, or Server 2008/2012. If not already installed, install it from the official [Visual C++ Redistributable](https://www.microsoft.com/en-in/download/details.aspx?id=48145) or include the required DLLs with your installer.
{% endhint %}

### Setting product.dat file and product id

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()`  function or set the absolute path of the file using `SetProductFile()`  function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```c
SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
SetProductId("PASTE_PRODUCT_ID", LA_USER);
```

If your app requires admin (root) privileges to run (e.g. services, daemons etc.), instead of passing `LA_USER` flag, you need to pass `LA_SYSTEM` flag.

If your app requires a single activation to be shared across all OS users (system-wide activation), pass the `LA_ALL_USERS` flag before activation. This flag is compatible with Windows OS only.

{% hint style="info" %}
In case your app doesn't have write access to the disk, you can use `LA_IN_MEMORY` flag instead, which causes all the data to be stored in the memory. But this would require you to activate the license every time you restart the app.
{% endhint %}

### License activation

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```c
int status;
status = SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
if (LA_OK != status)
{
	// handle error
}
status = SetProductId("PASTE_PRODUCT_ID", LA_USER);
if (LA_OK != status)
{
	// handle error
}
status = SetLicenseKey("PASTE_LICENCE_KEY");
if (LA_OK != status)
{
	 // handle error
}
status = SetActivationMetadata("key1", "value1");
if (LA_OK != status)
{
	 // handle error
}
status = ActivateLicense();
if (LA_OK == status || LA_EXPIRED == status || LA_SUSPENDED == status)
{
	printf("License activated successfully: %d", status);
}
else
{
	printf("License activation failed: %d", status);
}
```

The above code should be executed at the time of license activation, ideally on a button click.

### Verifying license activation

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this, you need to use `IsLicenseGenuine()` LexActivator API function.

```c
int status;
status = SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
if (LA_OK != status)
{
	// handle error
}
status = SetProductId("PASTE_PRODUCT_ID", LA_USER);
if (LA_OK != status)
{
	// handle error
}
status = IsLicenseGenuine();
if (LA_OK == status || LA_EXPIRED == status || LA_SUSPENDED == status  || LA_GRACE_PERIOD_OVER == status)
{
	printf("License is genuinely activated: %d", status);
}
else
{
	printf("License is not activated: %d", status);
}
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help

In case you need more help with adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).
