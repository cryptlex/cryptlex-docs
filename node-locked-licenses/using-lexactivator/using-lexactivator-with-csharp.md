# Using LexActivator with C\#

First of all, login to your Cryptlex account and download LexActivator library for Windows, MacOS or Linux:

* ​[Download LexActivator for Windows](https://app.cryptlex.com/downloads)​
* ​[Download LexActivator for MacOS](https://app.cryptlex.com/downloads)
* ​[Download LexActivator for Linux](https://app.cryptlex.com/downloads)​

The above download package contains the library which you will be using to add licensing to your app.

## Adding licensing to your app <a id="adding-licensing-to-your-app"></a>

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the Product.dat for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-csharp).

Product.dat contains product data which is used by LexActivator. Product id is the identifier of your product which is to be used in the code.

### Adding library to your app <a id="adding-library-to-your-app"></a>

LexActivator example project for C\# contains **LexActivator.cs** file. You will need to add this file to your C\# project. It contains all the LexActivator API functions needed to add licensing to your app.

Depending on the platform you are targeting **\(x86, x64 or AnyCPU\)** you need to copy the respective LexActivator.dll to the Debug and Release folders of your project.

{% hint style="info" %}
In case you choose **AnyCPU** Platform, you will need to copy both x86 LexActivator.dll and x64 LexActivator.dll \(renamed as LexActivator64.dll\) to your project. Additionally, you will have to add `LA_ANY_CPU` conditional compilation symbol in your project properties.
{% endhint %}

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

```csharp
private void activateLicenseBtn_Click(object sender, EventArgs e)
{
    int status;
    status = LexActivator.SetLicenseKey(productKeyBox.Text);
    if (status != LexActivator.StatusCodes.LA_OK)
    {
        // handle error
    }
    status = LexActivator.SetActivationMetadata("key1", "value1");
    if (status != LexActivator.StatusCodes.LA_OK)
    {
         // handle error
    }
    status = LexActivator.ActivateLicense();
    if (status == LexActivator.StatusCodes.LA_OK || status == LexActivator.StatusCodes.LA_EXPIRED || status == LexActivator.StatusCodes.LA_SUSPENDED)
    {
        // Activation successful
    }
    else
    {
        // Activation failed
    }
}
```

The above code should be executed at the time of license activation.

### Verifying license activation <a id="verifying-license-activation"></a>

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this you need to use `IsLicenseGenuine()` LexActivator API function.

```csharp
public ActivationForm()
{
    InitializeComponent();
    int status;
    status = LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
    if (status != LexActivator.StatusCodes.LA_OK)
    {
        this.statusLabel.Text = "Error setting product data: " + status.ToString();
        return;
    }
    status = LexActivator.SetProductId("PASTE_PRODUCT_ID", LexActivator.PermissionFlags.LA_USER);
    if (status != LexActivator.StatusCodes.LA_OK)
    {
        this.statusLabel.Text = "Error setting product id: " + status.ToString();
        return;
    }
    status = LexActivator.IsLicenseGenuine();
    if(status == LexActivator.StatusCodes.LA_OK || status == LexActivator.StatusCodes.LA_EXPIRED || status == LexActivator.StatusCodes.LA_SUSPENDED || status == LexActivator.StatusCodes.LA_GRACE_PERIOD_OVER)
    {
        this.statusLabel.Text = "License is activated: " + status.ToString();
    }
    else
    {
        this.statusLabel.Text = "License is not activated: " + status.ToString();
    }
}
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help <a id="need-more-help"></a>

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

