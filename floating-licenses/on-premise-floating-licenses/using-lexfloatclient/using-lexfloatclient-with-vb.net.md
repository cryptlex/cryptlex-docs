# Using LexFloatClient with VB.NET

First of all, login to your Cryptlex account and download LexFloatClient library for Windows:

* [Download LexFloatClient for Windows](https://app.cryptlex.com/downloads)

The above download package contains the library which you will be using to add licensing to your app.

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-vb.net)

Product id is the identifier of your product which is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding library to your app

LexFloatClient example project for VB.NET contains **LexFloatClient.vb** file. You will need to add this file to your VB.NET project. It contains all the LexFloatClient API functions needed to add licensing to your app.

Depending on the platform you are targeting **\(x86, x64 or AnyCPU\)** you need to copy the respective LexFloatClient.dll to the Debug and Release folders of your project.

{% hint style="info" %}
In case you choose **AnyCPU** Platform, you will need to copy both x86 LexFloatClient.dll and x64 LexFloatClient.dll \(renamed as LexFloatClient64.dll\) to your project. Additionally, you will have to add \(uncomment\) `LF_ANY_CPU = 1`custom constant in **LexFloatClient.vb** file.
{% endhint %}

### Setting product id

The first LexFloatClient API function you need to use in your code is `SetProductId()`. It sets the product id of the product you will be adding licensing to. 

```c
floatClient = New LexFloatClient()
floatClient.SetProductId("PASTE_PRODUCT_ID")
```

### Requesting license lease

To receive a floating license, you will use `SetFloatServer()`, `SetLicenseCallback()` and `RequestLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for status notifications, contacts the server and receives the leased license.

```csharp
Private Sub leaseBtn_Click(sender As Object, e As EventArgs) Handles leaseBtn.Click
    Dim status As Integer
    floatClient = New LexFloatClient()
    status = floatClient.SetProductId("PASTE_PRODUCT_ID")
    If status <> LexFloatClient.StatusCodes.LF_OK Then
        Me.statusLabel.Text = "Error setting version GUID: " + status.ToString()
        Return
    End If
    status = floatClient.SetFloatServer("localhost", 8090)
    If status <> LexFloatClient.StatusCodes.LF_OK Then
        Me.statusLabel.Text = "Error Setting Host Address: " + status.ToString()
        Return
    End If
    status = floatClient.SetLicenseCallback(AddressOf LicenceRefreshCallback)
    If status <> LexFloatClient.StatusCodes.LF_OK Then
        Me.statusLabel.Text = "Error Setting Callback Function: " + status.ToString()
        Return
    End If
    status = floatClient.RequestLicense()
    If status <> LexFloatClient.StatusCodes.LF_OK Then
        Me.statusLabel.Text = "Error Requesting License: " + status.ToString()
        Return
    End If
    Me.statusLabel.Text = "License leased successfully!"
End Sub
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing license lease

License lease automatically renews itself in a background thread. When something goes wrong, Callback is invoked \(from background thread\).

```csharp
Private Sub LicenceRefreshCallback(status As UInteger)
    Select Case status
        Case LexFloatClient.StatusCodes.LF_E_LICENSE_EXPIRED
            Me.statusLabel.Text = "The lease expired before it could be renewed."
            Exit Select
        Case LexFloatClient.StatusCodes.LF_E_LICENSE_EXPIRED_INET
            Me.statusLabel.Text = "The lease expired due to network connection failure."
            Exit Select
        Case LexFloatClient.StatusCodes.LF_E_SERVER_TIME
            Me.statusLabel.Text = "The lease expired because Server System time was modified."
            Exit Select
        Case LexFloatClient.StatusCodes.LF_E_TIME
            Me.statusLabel.Text = "The lease expired because Client System time was modified."
            Exit Select
        Case Else
            Me.statusLabel.Text = "The lease expired due to some other reason."
            Exit Select
    End Select
End Sub
```

You would usually request for a new license if callback gets invoked.

### Dropping license lease

When your user is done using the app, the app should send a request to free the license, thereby making it available for other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```csharp
Private Sub dropBtn_Click(sender As Object, e As EventArgs) Handles dropBtn.Click
    Dim status As Integer
    status = floatClient.DropLicense()
    If status <> LexFloatClient.StatusCodes.LF_OK Then
        Me.statusLabel.Text = "Error Dropping License: " + status.ToString()
	Else
		Me.statusLabel.Text = "License dropped successfully!"
	End If
    LexFloatClient.GlobalCleanUp()
End Sub
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://cryptlex.com/forums) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

