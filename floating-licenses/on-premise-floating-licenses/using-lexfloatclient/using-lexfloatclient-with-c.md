# Using LexFloatClient with C\#

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-dotnet/tree/master/examples).

Product id is the identifier of your product which is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding library to your app

LexFloatClient wrapper for C\# can be easily installed through [nuget](https://www.nuget.org/packages/Cryptlex.LexFloatClient):

```bash
Install-Package Cryptlex.LexFloatClient
# or
dotnet add package Cryptlex.LexFloatClient
```

LexFloatClient has dependency on `VS2015` runtime on **Windows**. On the target machines where you will deploy your app, you can install the `VS2015` runtime, if not present, using the link: [https://www.microsoft.com/en-in/download/details.aspx?id=48145](https://www.microsoft.com/en-in/download/details.aspx?id=48145)

LexFloatClient \(`.NET Core`\) has dependency on `libnss3` library on **Linux**. On the target machines where you will deploy your app, ensure `libnss3` library is installed.

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
    try
    {
        LexFloatClient.SetHostProductId("PASTE_YOUR_PRODUCT_ID");
        LexFloatClient.SetHostUrl("http://localhost:8090");
        LexFloatClient.SetFloatingLicenseCallback(LicenceRenewCallback);
        LexFloatClient.RequestFloatingLicense();
        this.statusLabel.Text = "License leased successfully!";
    }
    catch (LexFloatClientException ex)
    {
        this.statusLabel.Text = "Error code: " + ex.Code.ToString() + " Error message: " + ex.Message;
    }
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
        case LexFloatStatusCodes.LF_OK:
            this.statusLabel.Text = "The license lease has renewed successfully.";
            break;
        case LexFloatStatusCodes.LF_E_LICENSE_NOT_FOUND:
            this.statusLabel.Text = "The license expired before it could be renewed.";
            break;
        case LexFloatStatusCodes.LF_E_LICENSE_EXPIRED_INET:
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
    try
    {
        if (!LexFloatClient.HasFloatingLicense())
        {
            return;
        }
        LexFloatClient.DropFloatingLicense();
        this.statusLabel.Text = "License dropped successfully!";
    }
    catch (LexFloatClientException ex)
    {
        this.statusLabel.Text = "Error code: " + ex.Code.ToString() + " Error message: " + ex.Message;
    }
}
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help for adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

