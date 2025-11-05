# Using LexActivator with Python

## Adding licensing to your app <a href="#adding-licensing-to-your-app" id="adding-licensing-to-your-app"></a>

After you've added a product for your app in the admin portal, you will need to do the following things:

* Note the product id for the product (from the actions menu in the table).
* Download the Product.dat for the product (from the actions menu in the table).
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-python/tree/master/examples)

Product.dat contains product data that is used by LexActivator. The product id is the identifier of your product that is to be used in the code.

### Adding the library to your app <a href="#adding-library-to-your-app" id="adding-library-to-your-app"></a>

LexActivator wrapper for Python can be easily installed through [pip](https://pypi.org/project/cryptlex.lexactivator/):

```bash
pip install cryptlex.lexactivator
```

{% hint style="info" %}
**LexActivator** requires the Microsoft Visual C++ 2015 (or later) Runtime on older Windows versions such as Windows 7, 8, or Server 2008/2012. If not already installed, install it from the official [Visual C++ Redistributable](https://www.microsoft.com/en-in/download/details.aspx?id=48145) or include the required DLLs with your installer.
{% endhint %}

### Setting product.dat file and product Id <a href="#setting-product.dat-file-and-product-id" id="setting-product.dat-file-and-product-id"></a>

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```csharp
LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
LexActivator.SetProductId("PASTE_PRODUCT_ID", PermissionFlags.LA_USER);
```

If your app requires admin (root) privileges to run (e.g. services, daemons etc.), instead of passing   `PermissionFlags.LA_USER` flag, you need to pass `PermissionFlags.LA_SYSTEM` flag.

If your app requires a single activation to be shared across all OS users (system-wide activation), pass the `PermissionFlags.LA_ALL_USERS` flag before activation. This flag is compatible with Windows OS only.

{% hint style="info" %}
In case your app doesn't have write access to the disk, you can use `PermissionFlags.LA_IN_MEMORY` flag instead, which causes all the data to be stored in the memory. But this would require you to activate the license every time you restart the app.
{% endhint %}

### License activation <a href="#license-activation" id="license-activation"></a>

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```python
def activate():
    try:
        LexActivator.SetLicenseKey("PASTE_LICENCE_KEY")
        LexActivator.SetActivationMetadata("key1", "value1")
        status = LexActivator.ActivateLicense()
        if LexStatusCodes.LA_OK == status or LexStatusCodes.LA_EXPIRED == status or LexStatusCodes.LA_SUSPENDED == status:
            print("License activated successfully: ", status)
        else:
            print("License activation failed: ", status)
    except LexActivatorException as exception:
        print('Error code:', exception.code, exception.message)
```

The above code should be executed at the time of license activation.

### Verifying license activation <a href="#verifying-license-activation" id="verifying-license-activation"></a>

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this, you need to use `IsLicenseGenuine()` LexActivator API function.

```python
def main():
    try:
        LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE")
        LexActivator.SetProductId("PASTE_PRODUCT_ID", PermissionFlags.LA_USER)
        status = LexActivator.IsLicenseGenuine()
        if LexStatusCodes.LA_OK == status:
            print("License is genuinely activated!")
        elif LexStatusCodes.LA_EXPIRED == status:
            print("License is genuinely activated but has expired!")
        elif LexStatusCodes.LA_SUSPENDED == status:
            print("License is genuinely activated but has been suspended!")
        elif LexStatusCodes.LA_GRACE_PERIOD_OVER == status:
            print("License is genuinely activated but grace period is over!")
        else:
            print("License is not activated: ", status)
    except LexActivatorException as exception:
        print('Error code:', exception.code, exception.message)
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help <a href="#need-more-help" id="need-more-help"></a>

In case you need more help with adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).
