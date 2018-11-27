# Using LexActivator with Python

First of all, login to your Cryptlex account and download LexActivator library for Windows, MacOS or Linux:

* ​[Download LexActivator for Windows](https://app.cryptlex.com/downloads)​
* ​[Download LexActivator for MacOS](https://app.cryptlex.com/downloads)
* ​[Download LexActivator for Linux](https://app.cryptlex.com/downloads)​

The above download package contains the library which you will be using to add licensing to your app.

## Adding licensing to your app <a id="adding-licensing-to-your-app"></a>

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the Product.dat for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-python)

Product.dat contains product data which is used by LexActivator. Product id is the identifier of your product which is to be used in the code.

### Adding library to your app <a id="adding-library-to-your-app"></a>

LexActivator example project for Python contains **LexActivator.py** file. You will need to add this file to your Python project. It contains all the LexActivator API functions needed to add licensing to your app. Depending on the OS you are targeting you need to copy the respective LexActivator.dll, libLexActivator.so or libLexActivator.dylib to your project.

### Setting product.dat file and product Id <a id="setting-product.dat-file-and-product-id"></a>

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```csharp
LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
LexActivator.SetProductId("PASTE_PRODUCT_ID", LexActivator.PermissionFlags.LA_USER);
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing   `LexActivator.PermissionFlags.LA_USER` flag, you need to pass `LexActivator.PermissionFlags.LA_SYSTEM` flag.

### License activation <a id="license-activation"></a>

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```python
def activate():
    status = LexActivator.SetLicenseKey("PASTE_LICENCE_KEY")
    if LexActivator.StatusCodes.LA_OK != status:
        # handle error

    status = LexActivator.SetActivationMetadata("key1", "value1")
    if LexActivator.StatusCodes.LA_OK != status:
        # handle error

    status = LexActivator.ActivateLicense()
    if LexActivator.StatusCodes.LA_OK == status | LexActivator.StatusCodes.LA_EXPIRED == status | LexActivator.StatusCodes.LA_SUSPENDED == status:
        print("License activated successfully: ", status)
    else:
        print("License activation failed: ", status)
    return
```

The above code should be executed at the time of license activation.

### Verifying license activation <a id="verifying-license-activation"></a>

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this you need to use `IsLicenseGenuine()` LexActivator API function.

```python
def main():
    status = LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE")
    if LexActivator.StatusCodes.LA_OK != status:
        print("Error code: ", status)
        sys.exit(status)

    status = LexActivator.SetProductId("PASTE_PRODUCT_ID",
                                       LexActivator.PermissionFlags.LA_USER)
    if LexActivator.StatusCodes.LA_OK != status:
        print("Error code: ", status)
        sys.exit(status)

    status = LexActivator.SetAppVersion("PASTE_YOUR_APP_VERION")
    if LexActivator.StatusCodes.LA_OK != status:
        print("Error code: ", status)
        sys.exit(status)
    
    status = LexActivator.IsLicenseGenuine()
    if LexActivator.StatusCodes.LA_OK == status:
        expiryDate = ctypes.c_uint()
        LexActivator.GetLicenseExpiryDate(ctypes.byref(expiryDate))
        daysLeft = (expiryDate.value - time.time()) / 86500
        print("Days left: ", daysLeft)
        print("License is genuinely activated!")
    elif LexActivator.StatusCodes.LA_EXPIRED == status:
        print("License is genuinely activated but has expired!")
    elif LexActivator.StatusCodes.LA_SUSPENDED == status:
        print("License is genuinely activated but has been suspended!")
    elif LexActivator.StatusCodes.LA_GRACE_PERIOD_OVER == status:
        print("License is genuinely activated but grace period is over!")
    else:
        print("License is not activated: ",status)
    return
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help <a id="need-more-help"></a>

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

