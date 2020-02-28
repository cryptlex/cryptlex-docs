# Using LexActivator with Node.js

## Adding licensing to your app <a id="adding-licensing-to-your-app"></a>

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do three things:

* Note the product id for the product.
* Download the Product.dat for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-js/tree/master/examples).

Product.dat contains product data which is used by LexActivator. Product id is the identifier of your product which is to be used in the code.

{% hint style="info" %}
In order to package your Node.js project into an executable, check out [pkg](https://github.com/zeit/pkg) project.
{% endhint %}

### Adding library to your app <a id="adding-library-to-your-app"></a>

LexActivator wrapper for Node.js can be easily installed through [npm](https://www.npmjs.com/package/@cryptlex/lexactivator):

```bash
npm i @cryptlex/lexactivator 
```

**Note:** On Windows make sure you install the `windows-build-tools` package on the machine where you will build your app:

```bash
npm install --global windows-build-tools --vs2015
```

LexActivator has dependency on `VS2015` runtime on **Windows**. On the target machines where you will deploy your app, you can install the `VS2015` runtime, if not present, using the link: [https://www.microsoft.com/en-in/download/details.aspx?id=48145](https://www.microsoft.com/en-in/download/details.aspx?id=48145)

LexActivator has dependency on `libnss3` library on **Linux**. On the target machines where you will deploy your app, ensure `libnss3` library is installed.

### Setting product.dat file and product Id <a id="setting-product.dat-file-and-product-id"></a>

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```csharp
LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
LexActivator.SetProductId("PASTE_PRODUCT_ID", PermissionFlags.LA_USER);
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing   `PermissionFlags.LA_USER` flag, you need to pass `PermissionFlags.LA_SYSTEM` flag.

{% hint style="info" %}
In case your app doesn't have write access to the disk, you can use `PermissionFlags.LA_IN_MEMORY` flag instead, which causes all the data to be stored in the memory. But this would require you to activate the license every time you restart the app.
{% endhint %}

### License activation <a id="license-activation"></a>

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```javascript
function activate() {
    try {
      LexActivator.SetLicenseKey('PASTE_LICENCE_KEY');
	    LexActivator.SetActivationMetadata('key1', 'value1');
	    const status = LexActivator.ActivateLicense();
	    if (LexStatusCodes.LA_OK == status) {
		    console.log('License activated successfully!');
	    } else if (LexStatusCodes.LA_EXPIRED == status) {
		    console.log('License activated successfully but has expired!');
	    } else if (LexStatusCodes.LA_SUSPENDED == status) {
		    console.log('License activated successfully but has been suspended!');
	    }
    } catch(error) {
        console.log('License activated failed:', error.code, error.message);
    }
}
```

The above code should be executed at the time of license activation.

### Verifying license activation <a id="verifying-license-activation"></a>

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this you need to use `IsLicenseGenuine()` LexActivator API function.

```javascript
function main() {
    try {
        LexActivator.SetProductData('PASTE_CONTENT_OF_PRODUCT.DAT_FILE');
	    LexActivator.SetProductId('PASTE_PRODUCT_ID', PermissionFlags.LA_USER);
	    LexActivator.SetAppVersion('PASTE_YOUR_APP_VERION');
	    const status = LexActivator.IsLicenseGenuine();
        if (LexStatusCodes.LA_OK == status) {
            console.log("License is genuinely activated!");
        } else if (LexStatusCodes.LA_EXPIRED == status) {
            console.log("License is genuinely activated but has expired!");
        } else if (LexStatusCodes.LA_SUSPENDED == status) {
            console.log("License is genuinely activated but has been suspended!");
        } else if (LexStatusCodes.LA_GRACE_PERIOD_OVER == status) {
            console.log("License is genuinely activated but grace period is over!");
        } else {
             console.log("License is not activated:", status);
        }
    } catch (error) {
        console.log('Error:', error.code, error.message);
    }
}
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help <a id="need-more-help"></a>

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

