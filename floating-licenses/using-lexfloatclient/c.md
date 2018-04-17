# C\#

First of all, login to your Cryptlex account and download LexFloatClient for Windows:

* [Download LexFloatClient for Windows](https://cryptlex.com/app/api)

The above download package includes an example project. It contains all the functions you will be using to add licensing to your app.

## Adding Licensing to your App

After you've added a product for your app in the dashboard, go to the version page of the product you will be adding licensing to. You will need to do two things:

* Download the Product.dat for the product version.
* Note the Version GUID for the product version.

![product-version](https://cryptlex.com/public/img/docs/version.png)

Product.dat contains version data which is used by LexFloatClient and is to be included in the same directory as your app. Version GUID is the identifier of your product version which is to be used in the code.

### Adding Library to your App

LexFloatClient example project for C\# contains**LexFloatClient.cs**file. You will need to add this file to your C\# project. It contains all the LexFloatClient API functions needed to add licensing to your app.

Depending on the platform you are targeting**\(x86, x64 or AnyCPU\)**you need to copy the respective LexFloatClient.dll to the Debug and Release folders of your project.

**Note:**In case you choose AnyCPU Platform, you will need to copy both x86 LexFloatClient.dll and x64 LexFloatClient.dll \(renamed as LexFloatClient64.dll\) to your project. Additionally, you will have to add`LF_ANY_CPU`conditional compilation symbol in your project properties.

### Setting Version GUID

The first LexFloatClient API function you need to use in your code is`SetVersionGUID()`. It sets the version GUID of the product you will be adding licensing to. If the Product.dat file is not present in the same directory as your app or has been renamed, you need to invoke`SetProductFile()`function first to set the path of the product file.

```c
    floatClient = new LexFloatClient();
    floatClient.SetVersionGUID("YOUR VERSION GUID");
```

### Requesting License Lease

To receive a floating license, you will use`SetFloatServer()`,`SetLicenseCallback()`and`RequestLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for error notifications, contacts the server and receives the leased license.

```c
 private void leaseBtn_Click(object sender, EventArgs e)
    {
        int status;
        floatClient = new LexFloatClient();
        status = floatClient.SetVersionGUID("YOUR VERSION GUID");
        if (status != LexFloatClient.LF_OK)
        {
            this.statusLabel.Text = "Error setting version GUID: " + status.ToString();
            return;
        }
        status = floatClient.SetFloatServer( "localhost", 8090);
        if (status != LexFloatClient.LF_OK)
        {
            this.statusLabel.Text = "Error Setting Host Address: " + status.ToString();
            return;
        }
        status = floatClient.SetLicenseCallback( LicenceRefreshCallback);
        if (status != LexFloatClient.LF_OK)
        {
            this.statusLabel.Text = "Error Setting Callback Function: " + status.ToString();
            return;
        }
        status = floatClient.RequestLicense();
        if (status != LexFloatClient.LF_OK)
        {
            this.statusLabel.Text = "Error Requesting License: " + status.ToString();
            return;
        }
        this.statusLabel.Text = "License leased successfully!";
    }
```

The above code can be executed everytime user starts the app or needs a new license.

### Renewing License Lease

License lease automatically renews itself in a background thread. When something goes wrong, Callback is invoked \(from background thread\).

```c
  private void LicenceRefreshCallback(uint status)
    {
        switch (status)
        {
            case LexFloatClient.LF_E_LICENSE_EXPIRED:
                this.statusLabel.Text = "The lease expired before it could be renewed.";
                break;
            case LexFloatClient.LF_E_LICENSE_EXPIRED_INET:
                this.statusLabel.Text = "The lease expired due to network connection failure.";
                break;
            case LexFloatClient.LF_E_SERVER_TIME:
                this.statusLabel.Text = "The lease expired because Server System time was modified.";
                break;
            case LexFloatClient.LF_E_TIME:
                this.statusLabel.Text = "The lease expired because Client System time was modified.";
                break;
            default:
                this.statusLabel.Text = "The lease expired due to some other reason.";
                break;
        }
    }
```

You would ideally request for a new license if Callback gets invoked.

### Dropping License Lease

When your user is done using the app, the app should send a request to free the license, thereby making it available for other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```c
 private void dropBtn_Click(object sender, EventArgs e)
    {
        int status;
        status = floatClient.DropLicense();
        if (status != LexFloatClient.LF_OK){
            this.statusLabel.Text = "Error Dropping License: " + status.ToString();
        }
        else {
            this.statusLabel.Text = "License dropped successfully!";
        }
        LexFloatClient.GlobalCleanUp();
    }
```

The above code should be executed everytime user closes the app.

## Need more help?

In case you need more help for adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our[support forum](https://cryptlex.com/forums)or can contact us through[email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

