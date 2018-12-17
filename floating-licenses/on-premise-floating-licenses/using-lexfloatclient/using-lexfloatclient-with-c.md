# Using LexFloatClient with C\#

First of all, login to your Cryptlex account and download LexFloatClient library for Windows, MacOS or Linux:

* [Download LexFloatClient for Windows](https://app.cryptlex.com/downloads)
* [Download LexFloatClient for MacOS](https://app.cryptlex.com/downloads)
* [Download LexFloatClient for Linux](https://app.cryptlex.com/downloads)

The above download package contains the library which you will be using to add licensing to your app.

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-csharp).

Product id is the identifier of your product which is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding library to your app

LexFloatClient example project for C\# contains **LexFloatClient.cs** file. You will need to add this file to your C\# project. It contains all the LexFloatClient API functions needed to add licensing to your app.

Depending on the platform you are targeting **\(x86, x64 or AnyCPU\)** you need to copy the respective LexFloatClient.dll to the Debug and Release folders of your project.

{% hint style="info" %}
In case you choose **AnyCPU** Platform, you will need to copy both x86 LexFloatClient.dll and x64 LexFloatClient.dll \(renamed as LexFloatClient64.dll\) to your project. Additionally, you will have to add `LF_ANY_CPU` conditional compilation symbol in your project properties.
{% endhint %}

### Setting product id

The first LexFloatClient API function you need to use in your code is `SetHostProductId()`. It sets the product id of the product you will be adding licensing to. 

```csharp
LexFloatClient.SetHostProductId("PASTE_PRODUCT_ID");
```

### Requesting floating license

To receive a floating license, you will use `SetHostUrl()`, `SetFloatingLicenseCallback()` and `RequestFloatingLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for status notifications, contacts the server and receives the floating license.

```csharp
private void leaseBtn_Click(object sender, EventArgs e)
{
    if (LexFloatClient.HasLicense() == LexFloatClient.StatusCodes.LF_OK)
    {
        return;
    }
    int status;
    status = LexFloatClient.SetHostProductId("PASTE_YOUR_PRODUCT_ID");
    if (status != LexFloatClient.StatusCodes.LF_OK)
    {
        this.statusLabel.Text = "Error setting product id: " + status.ToString();
        return;
    }
    status = LexFloatClient.SetHostUrl("http://localhost:8090");
    if (status != LexFloatClient.StatusCodes.LF_OK)
    {
        this.statusLabel.Text = "Error setting host url: " + status.ToString();
        return;
    }
    status = LexFloatClient.SetFloatingLicenseCallback(LicenceRenewCallback);
    if (status != LexFloatClient.StatusCodes.LF_OK)
    {
        this.statusLabel.Text = "Error setting callback function: " + status.ToString();
        return;
    }
    status = LexFloatClient.RequestFloatingLicense();
    if (status != LexFloatClient.StatusCodes.LF_OK)
    {
        this.statusLabel.Text = "Error requesting license: " + status.ToString();
        return;
    }
    this.statusLabel.Text = "License leased successfully!";
}
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing license lease

License lease automatically renews itself in a background thread. When license is renewed or it fails to renew, Callback is invoked \(from background thread\).

```csharp
private void LicenceRenewCallback(uint status)
{
    switch (status)
    {
        case LexFloatClient.StatusCodes.LF_OK:
            this.statusLabel.Text = "The license lease has renewed successfully.";
            break;
        case LexFloatClient.StatusCodes.LF_E_LICENSE_NOT_FOUND:
            this.statusLabel.Text = "The license expired before it could be renewed.";
            break;
        case LexFloatClient.StatusCodes.LF_E_LICENSE_EXPIRED_INET:
            this.statusLabel.Text = "The license expired due to network connection failure.";
            break;
        default:
            this.statusLabel.Text = "The license renew failed due to other reason. Error code: " + status.ToString();
            break;
    }
}
```

### Dropping floating license

When your user is done using the app, the app should send a request to free the license, thereby making it available to other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```csharp
private void dropBtn_Click(object sender, EventArgs e)
{
    if (LexFloatClient.HasLicense() != LexFloatClient.StatusCodes.LF_OK)
    {
        return;
    }
    int status;
    status = LexFloatClient.DropLicense();
    if (status != LexFloatClient.StatusCodes.LF_OK)
    {
        this.statusLabel.Text = "Error dropping license: " + status.ToString();
        return;
    }
    this.statusLabel.Text = "License dropped successfully!";
}
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help for adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

