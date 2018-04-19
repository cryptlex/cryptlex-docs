# Using LexActivator with C\#

First of all, login to your Cryptlex account and download LexActivator library for Windows, Mac OS X or Linux:

* ​[Download LexActivator for Windows](https://cryptlex.com/app/api)​
* ​[Download LexActivator for Mac OS X](https://cryptlex.com/app/api)​
* ​[Download LexActivator for Linux](https://cryptlex.com/app/api)​

The above download package contains the library \(shared as well as static\) which you will be using to add licensing to your app.

## Adding Licensing to your App {#adding-licensing-to-your-app}

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the Product.dat for the product.
* Download the example project from github

Product.dat contains product data which is used by LexActivator. Product id is the identifier of your product which is to be used in the code.

### Adding Library to your App {#adding-library-to-your-app}

LexActivator example project for C contains the **LexActivator.h** header file. In addition to that it includes **LexActivator.lib** file required in case of Windows. It contains all the LexActivator API functions needed to add licensing to your app.

Depending on the platform you are targeting **\(x86 or x64\)** you need to link the respective LexActivator.dll with your application.

### Setting Product.dat file and Product Id {#setting-product.dat-file-and-product-id}

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```text
SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");SetProductId("PASTE_PRODUCT_ID", LA_USER);
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing `LA_USER` flag, you need to pass `LA_SYSTEM` flag.

### License Activation {#license-activation}

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```text
int status;status = SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");if (LA_OK != status){	// handle error}status = SetProductId("PASTE_PRODUCT_ID", LA_USER);if (LA_OK != status){	// handle error}status = SetLicenseKey("PASTE_LICENCE_KEY");if (LA_OK != status){	 // handle error}status = SetActivationMetadata("key1", "value1");if (LA_OK != status){	 // handle error}status = ActivateLicense();if (LA_OK == status || LA_EXPIRED == status || LA_SUSPENDED == status || LA_USAGE_LIMIT_REACHED == status){	printf("License activated successfully: %d", status);}else{	printf("License activation failed: %d", status);}
```

The above code should be executed at the time of registration, ideally on a button click.

### Verifying License Activation {#verifying-license-activation}

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this you need to use `IsLicenseGenuine()` LexActivator API function.

```text
int status;status = SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");if (LA_OK != status){	// handle error}status = SetProductId("PASTE_PRODUCT_ID", LA_USER);if (LA_OK != status){	// handle error}status = IsLicenseGenuine();if (LA_OK == status || LA_EXPIRED == status || LA_SUSPENDED == status || LA_USAGE_LIMIT_REACHED == status){	printf("License is genuinely activated: %d", status);}else{	printf("License is not activated: %d", status);}
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need More Help {#need-more-help}

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://cryptlex.com/forums) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

