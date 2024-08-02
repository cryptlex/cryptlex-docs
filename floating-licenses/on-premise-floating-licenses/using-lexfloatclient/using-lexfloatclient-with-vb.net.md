# Using LexFloatClient with VB.NET

## Adding licensing to your app

After you've added a product for your app in the admin portal, you will need to do the following things:

* Note the product id for the product (from the actions menu in the table).
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-dotnet/tree/master/examples)

The product id is the identifier of your product that is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding the library to your app

LexFloatClient wrapper for VB.NET can be easily installed through [nuget](https://www.nuget.org/packages/Cryptlex.LexFloatClient):

```bash
Install-Package Cryptlex.LexFloatClient
```

LexFloatClient has a dependency on `VS2015` runtime on **Windows**. On the target machines where you will deploy your app, you can install the `VS2015` runtime, if not present, using the link: [https://www.microsoft.com/en-in/download/details.aspx?id=48145](https://www.microsoft.com/en-in/download/details.aspx?id=48145)

### Setting product id

The first LexFloatClient API function you need to use in your code is `SetHostProductId()`. It sets the product id of the product you will be adding licensing to.&#x20;

```c
LexFloatClient.SetHostProductId("PASTE_PRODUCT_ID");
```

### Requesting license lease

To receive a floating license, you will use `SetHostUrl()`, `SetFloatingLicenseCallback()` and `RequestFloatingLicense()`LexFloatClient API methods. It sets the LexFloatServer address, the callback for status notifications, contacts the server and receives the floating license.

```csharp
Private Sub leaseBtn_Click(sender As Object, e As EventArgs) Handles leaseBtn.Click
    Try
        LexFloatClient.SetHostProductId("PASTE_YOUR_PRODUCT_ID")
        LexFloatClient.SetHostUrl("http://localhost:8090")
        LexFloatClient.SetFloatingLicenseCallback(AddressOf LicenceRenewCallback)
        LexFloatClient.RequestFloatingLicense()
        Me.statusLabel.Text = "License leased successfully!"
    Catch ex As LexFloatClientException
        Me.statusLabel.Text = "Error code: " & ex.Code.ToString() & " Error message: " + ex.Message
    End Try
End Sub
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing floating license

License lease automatically renews itself in a background thread. When a license is renewed or fails to renew, the callback is invoked (from the background thread).

```csharp
Private Sub LicenceRenewCallback(ByVal status As UInteger)
    Select Case status
        Case LexFloatStatusCodes.LF_OK
            Me.statusLabel.Text = "The license lease has renewed successfully."
            Exit Select
        Case LexFloatStatusCodes.LF_E_LICENSE_NOT_FOUND
            Me.statusLabel.Text = "The license expired before it could be renewed."
            Exit Select
        Case LexFloatStatusCodes.LF_E_LICENSE_EXPIRED_INET
            Me.statusLabel.Text = "The license expired due to network connection failure."
            Exit Select
        Case Else
            Me.statusLabel.Text = "The license renew failed due to other reason. Error code: " & status.ToString()
            Exit Select
    End Select
End Sub
```

### Dropping floating license

When your user is done using the app, the app should send a request to free the license, thereby making it available to other users. If the app doesn't, the license becomes (zombie) useless until lease time is over.

```csharp
Private Sub dropBtn_Click(sender As Object, e As EventArgs) Handles dropBtn.Click
    Try
        If Not LexFloatClient.HasFloatingLicense() Then
            Return
        End If
        LexFloatClient.DropFloatingLicense()
        Me.statusLabel.Text = "License dropped successfully!"
    Catch ex As LexFloatClientException
        Me.statusLabel.Text = "Error code: " & ex.Code.ToString() & " Error message: " + ex.Message
    End Try
End Sub
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help with adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).
