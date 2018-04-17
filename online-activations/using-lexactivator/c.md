# C\#

First of all, login to your Cryptlex account and download LexActivator for Windows:

* [Download LexActivator for Windows](https://cryptlex.com/app/api)

The above download package includes an example project. It contains all the functions you will be using to add licensing to your app.

## Adding Licensing to your App

After you've added a product for your app in the dashboard, go to the version page of the product you will be adding licensing to. You will need to do two things:

* Download the Product.dat for the product version.
* Note the Version GUID for the product version.

![product-version](https://cryptlex.com/public/img/docs/version.png)

Product.dat contains version data which is used by LexActivator and is to be included in the same directory as your app. Version GUID is the identifier of your product version which is to be used in the code.

### Adding Library to your App

LexActivator example project for C\# contains**LexActivator.cs**file. You will need to add this file to your C\# project. It contains all the LexActivator API functions needed to add licensing to your app.

Depending on the platform you are targeting**\(x86, x64 or AnyCPU\)**you need to copy the respective LexActivator.dll to the Debug and Release folders of your project.

**Note:**In case you choose AnyCPU Platform, you will need to copy both x86 LexActivator.dll and x64 LexActivator.dll \(renamed as LexActivator64.dll\) to your project. Additionally, you will have to add`LA_ANY_CPU`conditional compilation symbol in your project properties.

### Setting Version GUID

The first LexActivator API function you need to use in your code is`SetVersionGUID()`. It sets the version GUID of the product you will be adding licensing to. If the Product.dat file is not present in the same directory as your app or has been renamed, you need to invoke`SetProductFile()`function first to set the path of the product file.

```c
  LexActivator.SetVersionGUID("YOUR VERSION GUID", LexActivator.PermissionFlags.LA_USER);
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing`LexActivator.PermissionFlags.LA_USER`flag, you need to pass`LexActivator.PermissionFlags.LA_SYSTEM`flag.

### Online Activation

To activate your app using the product key, you will use`ActivateProduct()`LexActivator API function. It contacts the Cryptlex servers, validates the key and returns with encrypted and digitally signed response which it stores and uses to activate the product.

```c
    private void activateBtn_Click(object sender, EventArgs e)
    {
        int status;
        status = LexActivator.SetProductKey("YOUR PRODUCT KEY");
        if (status != LexActivator.LA_OK)
        {
            this.statusLabel.Text = "Error setting product key: " + status.ToString();
            return;
        }
        LexActivator.SetExtraActivationData("sample data");
        status = LexActivator.ActivateProduct();
        if (status == LexActivator.LA_OK)
        {
            this.statusLabel.Text = "Activation successful";
        }
        else if (status == LexActivator.LA_EXPIRED)
        {
            this.statusLabel.Text = "Activation successful, but license validity has expired!";
        }
        else
        {
            this.statusLabel.Text = "Error activating the product: " + status.ToString();
        }
    }
```

The above code should be executed at the time of registration.

### Verifying Activation

Each time, your app starts, you need to verify whether your app is already activated or not. This verification should occur locally by verifying the cryptographic digital signature fetched at the time of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate the activation periodically. For this you need to use`IsProductGenuine()`LexActivator API function.

```c
  public Form1()
    {
        InitializeComponent();
        int status;
        status = LexActivator.SetVersionGUID("YOUR VERSION GUID", LexActivator.PermissionFlags.LA_USER);
        if (status != LexActivator.LA_OK)
        {
            this.statusLabel.Text = "Error setting version GUID: " + status.ToString();
            return;
        }
        status = LexActivator.IsProductGenuine();
        if(status == LexActivator.LA_OK)
        {
            this.statusLabel.Text = "Product genuinely activated!";
        }
        else if(status == LexActivator.LA_EXPIRED)
        {
            this.statusLabel.Text = "Product is genuinely activated, but license validity has expired!";
        }
        else if(status == LexActivator.LA_GP_OVER)
        {
            this.statusLabel.Text = "Product is genuinely activated, but grace period is over!";
        }
        else
        {
            this.statusLabel.Text = "Product is not activated!";
        }
    }
```

The above code should be executed everytime user starts the app. After verifying locally, it schedules a server check in a separate thread.

## Need more help?

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our[support forum](https://cryptlex.com/forums)or can contact us through[email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

