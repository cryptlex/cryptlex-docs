# Using LexActivator with iOS

First of all, login to your Cryptlex account and download the LexActivator library for iOS:

* [Download LexActivator for iOS](https://app.cryptlex.com/downloads)

The above download package contains the library in the .xcframework format. The .xcframework supports the following architectures:

* iOS Simulator - x86\_64 \(Intel\), ARM64 \(Apple Silicon\) 
* iOS - ARM64

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the Product.dat for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-ios/tree/main/examples/sample).

Product.dat contains product data that is used by LexActivator. The product id is the identifier of your product that is to be used in the code.

### Adding the library to your app

After downloading the library in .xcframework format, just add it to your project in Xcode. You can add the dynamic as well as the static framework depending on your requirements.   

### Setting product.dat file and product id

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()`  function or set the absolute path of the file using `SetProductFile()`  function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```c
SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
SetProductId("PASTE_PRODUCT_ID", LA_USER);
```

{% hint style="info" %}
In case your app doesn't have write access to the disk, you can use `LA_IN_MEMORY` flag instead, which causes all the data to be stored in the memory. But this would require you to activate the license every time you restart the app.
{% endhint %}

### License activation

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```c
int status;
const char *licenseKey = [self.licenseKeyTextField.text UTF8String];
status = SetLicenseKey(licenseKey);
if(status != LA_OK)
{
    self.licenseStatusLabel.text = [NSString stringWithFormat:@"%d",status];
    return;
}
status = ActivateLicense();
self.licenseStatusLabel.text = [NSString stringWithFormat:@"License Status: %d",status];
```

The above code should be executed at the time of license activation, ideally on a button click.

### Verifying license activation

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this, you need to use `IsLicenseGenuine()` LexActivator API function.

```c
int status;
status = SetProductData("PASTE_PRODUCT_DATA");
if(status != LA_OK)
{
    self.licenseStatusLabel.text = [NSString stringWithFormat:@"%d",status];
    return;
}
status = SetProductId("PASTE_PRODUCT_ID", LA_USER);
if(status != LA_OK)
{
    self.licenseStatusLabel.text = [NSString stringWithFormat:@"%d",status];
    return;
}
status = IsLicenseGenuine();
if (LA_OK == status || LA_EXPIRED == status || LA_SUSPENDED == status  || LA_GRACE_PERIOD_OVER == status)
{
	  self.licenseStatusLabel.text = [NSString stringWithFormat:@"License is genuinely activated. Status: %d",status];
}
else
{
    self.licenseStatusLabel.text = [NSString stringWithFormat:@"License is not activated: %d",status];
}
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help

In case you need more help with adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

