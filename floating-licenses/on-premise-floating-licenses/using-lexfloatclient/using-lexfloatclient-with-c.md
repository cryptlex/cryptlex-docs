# Using LexFloatClient with C\#

First of all, login to your Cryptlex account and download LexFloatClient library for Windows, MacOS or Linux:

* [Download LexFloatClient for Windows](https://cryptlex.com/app/api)
* [Download LexFloatClient for MacOS](https://cryptlex.com/app/api)
* [Download LexFloatClient for Linux](https://cryptlex.com/app/api)

The above download package contains the library which you will be using to add licensing to your app.

## Adding Licensing to your App

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from github

Product id is the identifier of your product which is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding Library to your App

LexFloatClient example project for C\# contains **LexFloatClient.cs** file. You will need to add this file to your C\# project. It contains all the LexFloatClient API functions needed to add licensing to your app.

Depending on the platform you are targeting **\(x86, x64 or AnyCPU\)** you need to copy the respective LexFloatClient.dll to the Debug and Release folders of your project.

{% hint style="info" %}
In case you choose **AnyCPU** Platform, you will need to copy both x86 LexFloatClient.dll and x64 LexFloatClient.dll \(renamed as LexFloatClient64.dll\) to your project. Additionally, you will have to add `LF_ANY_CPU` conditional compilation symbol in your project properties.
{% endhint %}

### Setting Product Id

The first LexFloatClient API function you need to use in your code is `SetProductId()`. It sets the product id of the product you will be adding licensing to. 

```csharp
floatClient = new LexFloatClient();
floatClient.SetProductId("PASTE_PRODUCT_ID");
```

### Requesting License Lease

To receive a floating license, you will use `SetFloatServer()`, `SetLicenseCallback()` and `RequestLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for status notifications, contacts the server and receives the leased license.

```csharp
private void leaseBtn_Click(object sender, EventArgs e)
{
	int status;
	floatClient = new LexFloatClient();
	status = floatClient.SetProductId("PASTE_PRODUCT_ID");
	if (status != LexFloatClient.StatusCodes.LF_OK)
	{
		this.statusLabel.Text = "Error setting product id: " + status.ToString();
		return;
	}
	status = floatClient.SetFloatServer( "localhost", 8090);
	if (status != LexFloatClient.StatusCodes.LF_OK)
	{
		this.statusLabel.Text = "Error Setting Host Address: " + status.ToString();
		return;
	}
	status = floatClient.SetLicenseCallback( LicenceRefreshCallback);
	if (status != LexFloatClient.StatusCodes.LF_OK)
	{
		this.statusLabel.Text = "Error Setting Callback Function: " + status.ToString();
		return;
	}
	status = floatClient.RequestLicense();
	if (status != LexFloatClient.StatusCodes.LF_OK)
	{
		this.statusLabel.Text = "Error Requesting License: " + status.ToString();
		return;
	}
	this.statusLabel.Text = "License leased successfully!";
}
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing License Lease

License lease automatically renews itself in a background thread. When something goes wrong, Callback is invoked \(from background thread\).

```csharp
private void LicenceRefreshCallback(uint status)
{
    switch (status)
    {
        case LexFloatClient.StatusCodes.LF_E_LICENSE_EXPIRED:
            this.statusLabel.Text = "The lease expired before it could be renewed.";
            break;
        case LexFloatClient.StatusCodes.LF_E_LICENSE_EXPIRED_INET:
            this.statusLabel.Text = "The lease expired due to network connection failure.";
            break;
        case LexFloatClient.StatusCodes.LF_E_SERVER_TIME:
            this.statusLabel.Text = "The lease expired because Server System time was modified.";
            break;
        case LexFloatClient.StatusCodes.LF_E_TIME:
            this.statusLabel.Text = "The lease expired because Client System time was modified.";
            break;
        default:
            this.statusLabel.Text = "The lease expired due to some other reason.";
            break;
    }
}
```

You would usually request for a new license if callback gets invoked.

### Dropping License Lease

When your user is done using the app, the app should send a request to free the license, thereby making it available for other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```csharp
private void dropBtn_Click(object sender, EventArgs e)
{
    int status;
    status = floatClient.DropLicense();
    if (status != LexFloatClient.StatusCodes.LF_OK){
        this.statusLabel.Text = "Error Dropping License: " + status.ToString();
    }
    else {
        this.statusLabel.Text = "License dropped successfully!";
    }
    LexFloatClient.GlobalCleanUp();
}
```

The above code should be executed every time user closes the app.

## Need More Help

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://cryptlex.com/forums) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

