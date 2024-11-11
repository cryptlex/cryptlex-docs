# Using LexActivator with C\#

## Adding licensing to your app <a href="#adding-licensing-to-your-app" id="adding-licensing-to-your-app"></a>

After you've added a product for your app in the admin portal, you will need to do the following things:

* Note the product id for the product (from the actions menu in the table).
* Download the Product.dat for the product (from the actions menu in the table).
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-dotnet/tree/master/examples).

Product.dat contains product data that is used by LexActivator. The product id is the identifier of your product that is to be used in the code.

### Adding the library to your app <a href="#adding-library-to-your-app" id="adding-library-to-your-app"></a>

LexActivator wrapper for C# can be easily installed through [nuget](https://www.nuget.org/packages/Cryptlex.LexActivator/):

```bash
Install-Package Cryptlex.LexActivator
# or
dotnet add package Cryptlex.LexActivator
```

LexActivator has a dependency on `VS2015` runtime on **Windows**. On the target machines where you will deploy your app, you can install the `VS2015` runtime, if not present, using the link: [https://www.microsoft.com/en-in/download/details.aspx?id=48145](https://www.microsoft.com/en-in/download/details.aspx?id=48145)

### Setting product.dat file and product Id <a href="#setting-product.dat-file-and-product-id" id="setting-product.dat-file-and-product-id"></a>

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```csharp
LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
LexActivator.SetProductId("PASTE_PRODUCT_ID", LexActivator.PermissionFlags.LA_USER);
```

If your app requires admin (root) privileges to run (e.g. services, daemons etc.), instead of passing   `LexActivator.PermissionFlags.LA_USER` flag, you need to pass `LexActivator.PermissionFlags.LA_SYSTEM` flag.

If your app requires a single activation to be shared across all OS users (system-wide activation), pass the `LexActivator.PermissionFlags.LA_ALL_USERS` flag before activation. This flag is compatible with Windows OS only.

{% hint style="info" %}
In case your app doesn't have write access to the disk, you can use `LexActivator.PermissionFlags.LA_IN_MEMORY` flag instead, which causes all the data to be stored in the memory. But this would require you to activate the license every time you restart the app.
{% endhint %}

### License activation <a href="#license-activation" id="license-activation"></a>

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```csharp
private void activateLicenseBtn_Click(object sender, EventArgs e)
{
    try
    {
        int status;
        LexActivator.SetLicenseKey(productKeyBox.Text);
        status = LexActivator.ActivateLicense();
        if (status == LexStatusCodes.LA_OK || status == LexStatusCodes.LA_EXPIRED || status == LexStatusCodes.LA_SUSPENDED)
        {
            // Activation successful
        }
        else
        {
             // Activation failed
        }
    }
    catch (LexActivatorException ex)
    {
        // handle error
    }
}
```

The above code should be executed at the time of license activation.

### Verifying license activation <a href="#verifying-license-activation" id="verifying-license-activation"></a>

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this, you need to use `IsLicenseGenuine()` LexActivator API function.

```csharp
public ActivationForm()
{
    InitializeComponent();
    try
    {
        LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
        LexActivator.SetProductId("PASTE_PRODUCT_ID", LexActivator.PermissionFlags.LA_USER);
        int status = LexActivator.IsLicenseGenuine();
        if (status == LexStatusCodes.LA_OK || status == LexStatusCodes.LA_EXPIRED || status == LexStatusCodes.LA_SUSPENDED || status == LexStatusCodes.LA_GRACE_PERIOD_OVER)
        {
            this.statusLabel.Text = "License is activated: " + status.ToString();
        }
        else
        {
            this.statusLabel.Text = "License is not activated: " + status.ToString();
        }
    }
    catch (LexActivatorException ex)
    {
        this.statusLabel.Text = "Error code: " + ex.Code.ToString() + " Error message: " + ex.Message;
    }
}
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help <a href="#need-more-help" id="need-more-help"></a>

In case you need more help with adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).
