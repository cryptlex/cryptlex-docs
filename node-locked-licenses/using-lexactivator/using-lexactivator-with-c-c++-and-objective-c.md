# Using LexActivator with C, C++ & Objective C

First of all, login to your Cryptlex account and download LexActivator library for Windows, Mac OS X or Linux:

* [Download LexActivator for Windows](https://cryptlex.com/app/api)
* [Download LexActivator for Mac OS X](https://cryptlex.com/app/api)
* [Download LexActivator for Linux](https://cryptlex.com/app/api)

The above download package contains the library \(shared as well as static\) which you will be using to add licensing to your app.

## Adding Licensing to your App

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the Product.dat for the product.
* Download the example project from github

Product.dat contains product data which is used by LexActivator. Product id is the identifier of your product which is to be used in the code.

### Adding Library to your App

LexActivator example project for C contains the **LexActivator.h** header file. In addition to that it includes **LexActivator.lib **file required in case of Windows. It contains all the LexActivator API functions needed to add licensing to your app.

Depending on the platform you are targeting **\(x86 or x64\)** you need to link the respective LexActivator.dll with your application.

### Setting  Product.dat file and Product Id

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()`  function or set the absolute path of the file using `SetProductFile()`  function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```c
SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
SetProductId("PASTE_PRODUCT_ID", LA_USER);
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing `LA_USER` flag, you need to pass `LA_SYSTEM` flag.

### License Activation

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the  encrypted and digitally signed response to validate the license.

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
if (LA_OK == status || LA_EXPIRED == status || LA_SUSPENDED == status || LA_USAGE_LIMIT_REACHED == status)
{
	printf("License activated successfully: %d", status);
}
else
{
	printf("License activation failed: %d", status);
}
```

