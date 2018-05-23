# Using LexActivator with VB.NET

First of all, login to your Cryptlex account and download LexActivator library for Windows:

* ​[Download LexActivator for Windows](https://app.cryptlex.com/downloads)​

The above download package contains the library which you will be using to add licensing to your app.

## Adding licensing to your app {#adding-licensing-to-your-app}

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the Product.dat for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-vb.net)

Product.dat contains product data which is used by LexActivator. Product id is the identifier of your product which is to be used in the code.

### Adding library to your app {#adding-library-to-your-app}

LexActivator example project for VB.NET contains **LexActivator.vb** file. You will need to add this file to your VB.NET project. It contains all the LexActivator API functions needed to add licensing to your app.

Depending on the platform you are targeting **\(x86, x64 or AnyCPU\)** you need to copy the respective LexActivator.dll to the Debug and Release folders of your project.

{% hint style="info" %}
In case you choose **AnyCPU** Platform, you will need to copy both x86 LexActivator.dll and x64 LexActivator.dll \(renamed as LexActivator64.dll\) to your project. Additionally, you will have to add \(uncomment\) `LA_ANY_CPU = 1` custom constant in **LexActivator.vb** file.
{% endhint %}

### Setting product.dat file and product Id {#setting-product.dat-file-and-product-id}

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```csharp
LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
LexActivator.SetProductId("PASTE_PRODUCT_ID", LexActivator.PermissionFlags.LA_USER);
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing   `LexActivator.PermissionFlags.LA_USER` flag, you need to pass `LexActivator.PermissionFlags.LA_SYSTEM` flag.

### License activation {#license-activation}

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```csharp
Private Sub activateLicenseBtn_Click(ByVal sender As Object, ByVal e As EventArgs)
    Dim status As Integer
    status = LexActivator.SetLicenseKey(productKeyBox.Text)
    If status <> LexActivator.StatusCodes.LA_OK Then
        ' handle error
    End If

    status = LexActivator.SetActivationMetadata("key1", "value1")
    If status <> LexActivator.StatusCodes.LA_OK Then
        ' handle error
    End If

    status = LexActivator.ActivateLicense()
    If status = LexActivator.StatusCodes.LA_OK OrElse status = LexActivator.StatusCodes.LA_EXPIRED OrElse status = LexActivator.StatusCodes.LA_SUSPENDED Then
        ' activation successful
    Else
        ' activation failed
    End If
End Sub
```

The above code should be executed at the time of license activation.

### Verifying license activation {#verifying-license-activation}

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this you need to use `IsLicenseGenuine()` LexActivator API function.

```csharp
Public Sub New()
    InitializeComponent()
    Dim status As Integer
    status = LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE")
    If status <> LexActivator.StatusCodes.LA_OK Then
        Me.statusLabel.Text = "Error setting product data: " & status.ToString()
        Return
    End If

    status = LexActivator.SetProductId("PASTE_PRODUCT_ID", LexActivator.PermissionFlags.LA_USER)
    If status <> LexActivator.StatusCodes.LA_OK Then
        Me.statusLabel.Text = "Error setting product id: " & status.ToString()
        Return
    End If

    status = LexActivator.IsLicenseGenuine()
    If status = LexActivator.StatusCodes.LA_OK OrElse status = LexActivator.StatusCodes.LA_EXPIRED OrElse status = LexActivator.StatusCodes.LA_SUSPENDED OrElse status = LexActivator.StatusCodes.LA_GRACE_PERIOD_OVER Then
        Me.statusLabel.Text = "License is activated: " & status.ToString()
    Else
        Me.statusLabel.Text = "License is not activated: " & status.ToString()
    End If
End Sub
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help {#need-more-help}

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

