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

The first LexFloatClient API function you need to use in your code is `SetHostProductId()`. It sets the product id of the product you will be adding licensing to. 

```c
LexFloatClient.SetHostProductId("PASTE_PRODUCT_ID");
```

### Requesting license lease

To receive a floating license, you will use `SetHostUrl()`, `SetFloatingLicenseCallback()` and `RequestFloatingLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for status notifications, contacts the server and receives the floating license.

```csharp
Private Sub leaseBtn_Click(sender As Object, e As EventArgs) Handles leaseBtn.Click
    If LexFloatClient.HasLicense() = LexFloatClient.StatusCodes.LF_OK Then
        Return
    End If

    Dim status As Integer
    status = LexFloatClient.SetHostProductId("PASTE_YOUR_PRODUCT_ID")

    If status <> LexFloatClient.StatusCodes.LF_OK Then
        Me.statusLabel.Text = "Error setting product id: " & status.ToString()
        Return
    End If

    status = LexFloatClient.SetHostUrl("http://localhost:8090")

    If status <> LexFloatClient.StatusCodes.LF_OK Then
        Me.statusLabel.Text = "Error setting host url: " & status.ToString()
        Return
    End If

    status = LexFloatClient.SetFloatingLicenseCallback(LicenceRenewCallback)

    If status <> LexFloatClient.StatusCodes.LF_OK Then
        Me.statusLabel.Text = "Error setting callback function: " & status.ToString()
        Return
    End If

    status = LexFloatClient.RequestFloatingLicense()

    If status <> LexFloatClient.StatusCodes.LF_OK Then
        Me.statusLabel.Text = "Error requesting license: " & status.ToString()
        Return
    End If

    Me.statusLabel.Text = "License leased successfully!"
End Sub
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing floating license

License lease automatically renews itself in a background thread. When license is renewed or it fails to renew, Callback is invoked \(from background thread\).

```csharp
Private Sub LicenceRenewCallback(ByVal status As UInteger)
    Select Case status
        Case LexFloatClient.StatusCodes.LF_OK
            Me.statusLabel.Text = "The license lease has renewed successfully."
            Exit Select
        Case LexFloatClient.StatusCodes.LF_E_LICENSE_NOT_FOUND
            Me.statusLabel.Text = "The license expired before it could be renewed."
            Exit Select
        Case LexFloatClient.StatusCodes.LF_E_LICENSE_EXPIRED_INET
            Me.statusLabel.Text = "The license expired due to network connection failure."
            Exit Select
        Case Else
            Me.statusLabel.Text = "The license renew failed due to other reason. Error code: " & status.ToString()
            Exit Select
    End Select
End Sub
```

### Dropping floating license

When your user is done using the app, the app should send a request to free the license, thereby making it available to other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```csharp
Private Sub dropBtn_Click(sender As Object, e As EventArgs) Handles dropBtn.Click
    If LexFloatClient.HasLicense() <> LexFloatClient.StatusCodes.LF_OK Then
        Return
    End If

    Dim status As Integer
    status = LexFloatClient.DropLicense()

    If status <> LexFloatClient.StatusCodes.LF_OK Then
        Me.statusLabel.Text = "Error dropping license: " & status.ToString()
        Return
    End If

    Me.statusLabel.Text = "License dropped successfully!"
End Sub
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help for adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

