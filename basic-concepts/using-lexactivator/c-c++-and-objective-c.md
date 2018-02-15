## Using LexActivator with C, C++, and Objective-C

First of all, login to your Cryptlex account and download LexActivator for Windows, Mac OS X or Linux:

* [Download LexActivator for Windows](https://cryptlex.com/app/api)
* [Download LexActivator for Mac OS X](https://cryptlex.com/app/api)
* [Download LexActivator for Linux](https://cryptlex.com/app/api)

The above download package includes an example project. It contains all the functions you will be using to add licensing to your app.

### Adding Licensing to your App

After you've added a product for your app in the dashboard, go to the version page of the product you will be adding licensing to. You will need to do two things:

* Download the Product.dat for the product version.
* Note the Version GUID for the product version.

[![](https://cryptlex.com/public/img/docs/version.png "product-version")](https://cryptlex.com/public/img/docs/version.png)

Product.dat contains version data which is used by LexActivator and is to be included in the same directory as your app. Version GUID is the identifier of your product version which is to be used in the code.

#### Adding Library to your App

LexActivator example project for C contains the**LexActivator.h**header file. In addition to that it includes**LexActivator.lib**file required in case of Windows. It contains all the LexActivator API functions needed to add licensing to your app.

Depending on the platform you are targeting**\(x86 or x64\)**you need to link the respective LexActivator.dll with your application.

#### Setting Version GUID

The first LexActivator API function you need to use in your code is`SetVersionGUID()`. It sets the version GUID of the product you will be adding licensing to. If the Product.dat file is not present in the same directory as your app or has been renamed, you need to invoke`SetProductFile()`function first to set the path of the product file.

```c
SetVersionGUID("YOUR VERSION GUID", LA_USER);
    
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing`LA_USER`flag, you need to pass`LA_SYSTEM`flag.

#### Online Activation

To activate your app using the product key, you will use`ActivateProduct()`LexActivator API function. It contacts the Cryptlex servers, validates the key and returns with encrypted and digitally signed response which it stores and uses to activate the product.

```c
int status;
    status = SetProductKey("YOUR PRODUCT KEY");
	if(LA_OK != status) {
		printf("Error code: %d",status);
		getchar();
		return status;
	}
	SetExtraActivationData("sample data");
	// Activating the product
	status = ActivateProduct();    // Ideally on a button click inside a dialog
	if (LA_OK == status){
		printf("Activation successful!");
	}
    else if(LA_EXPIRED == status) {
        printf("Activation successful, but license validity has expired!");
    }
	else {
		printf("Error code: %d",status);
	}
```

The above code should be executed at the time of registration, ideally on a button click.

#### Verifying Activation

Each time, your app starts, you need to verify whether your app is already activated or not. This verification should occur locally by verifying the cryptographic digital signature fetched at the time of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate the activation periodically. For this you need to use`IsProductGenuine()`LexActivator API function.

```c
int status;
	status = SetVersionGUID("YOUR VERSION GUID", LA_USER);
	if(LA_OK != status) {
		printf("Error code: %d",status);
		getchar();
		return status;
	}
	status = IsProductGenuine();
	if(LA_OK == status) {
		printf("Product is genuinely activated!");
	}
	else if(LA_EXPIRED == status) {
		printf("Product is genuinely activated, but license validity has expired!");
	}
	else if(LA_GP_OVER == status) {
		printf("Product is genuinely activated, but grace period is over!");
	}
    else {
		printf("Product is not activated!");
	}
```

The above code should be executed everytime user starts the app. After verifying locally, it schedules a server check in a separate thread.

### Need more help?

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://cryptlex.com/forums) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

