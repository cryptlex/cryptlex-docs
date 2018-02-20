## Using LexFloatClient with VB.NET

First of all, login to your Cryptlex account and download LexFloatClient for Windows:

* [Download LexFloatClient for Windows](https://cryptlex.com/app/api)

The above download package includes an example project. It contains all the functions you will be using to add licensing to your app.

### Adding Licensing to your App

After you've added a product for your app in the dashboard, go to the version page of the product you will be adding licensing to. You will need to do two things:

* Download the Product.dat for the product version.
* Note the Version GUID for the product version.

[![](https://cryptlex.com/public/img/docs/version.png "product-version")](https://cryptlex.com/public/img/docs/version.png)

Product.dat contains version data which is used by LexFloatClient and is to be included in the same directory as your app. Version GUID is the identifier of your product version which is to be used in the code.

#### Adding Library to your App

LexFloatClient example project for VB.NET contains**LexFloatClient.vb**file. You will need to add this file to your VB.NET project. It contains all the LexFloatClient API functions needed to add licensing to your app.

Depending on the platform you are targeting**\(x86, x64 or AnyCPU\)**you need to copy the respective LexFloatClient.dll to the Debug and Release folders of your project.

**Note:**In case you choose AnyCPU Platform, you will need to copy both x86 LexFloatClient.dll and x64 LexFloatClient.dll \(renamed as LexFloatClient64.dll\) to your project. Additionally, you will have to add \(uncomment\)`LF_ANY_CPU = 1`custom constant in**LexFloatClient.vb**file.

#### Setting Version GUID

The first LexFloatClient API function you need to use in your code is`SetVersionGUID()`. It sets the version GUID of the product you will be adding licensing to. If the Product.dat file is not present in the same directory as your app or has been renamed, you need to invoke`SetProductFile()`function first to set the path of the product file.

```c

    floatClient = New LexFloatClient()
    floatClient.SetVersionGUID("YOUR VERSION GUID")
```



#### Requesting License Lease

To receive a floating license, you will use`SetFloatServer()`,`SetLicenseCallback()`and`RequestLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for error notifications, contacts the server and receives the leased license.

```c

    Private Sub leaseBtn_Click(sender As Object, e As EventArgs) Handles leaseBtn.Click
        Dim status As Integer
        floatClient = New LexFloatClient()
        status = floatClient.SetVersionGUID("59A44CE9-5415-8CF3-BD54-EA73A64E9A1B")
        If status <> LexFloatClient.LF_OK Then
            Me.statusLabel.Text = "Error setting version GUID: " + status.ToString()
            Return
        End If
        status = floatClient.SetFloatServer("localhost", 8090)
        If status <> LexFloatClient.LF_OK Then
            Me.statusLabel.Text = "Error Setting Host Address: " + status.ToString()
            Return
        End If
        status = floatClient.SetLicenseCallback(AddressOf LicenceRefreshCallback)
        If status <> LexFloatClient.LF_OK Then
            Me.statusLabel.Text = "Error Setting Callback Function: " + status.ToString()
            Return
        End If
        status = floatClient.RequestLicense()
        If status <> LexFloatClient.LF_OK Then
            Me.statusLabel.Text = "Error Requesting License: " + status.ToString()
            Return
        End If
        Me.statusLabel.Text = "License leased successfully!"
    End Sub
    
```

The above code can be executed everytime user starts the app or needs a new license.

#### Renewing License Lease

License lease automatically renews itself in a background thread. When something goes wrong, Callback is invoked \(from background thread\).

```c
  Private Sub LicenceRefreshCallback(status As UInteger)
        Select Case status
            Case LexFloatClient.LF_E_LICENSE_EXPIRED
                Me.statusLabel.Text = "The lease expired before it could be renewed."
                Exit Select
            Case LexFloatClient.LF_E_LICENSE_EXPIRED_INET
                Me.statusLabel.Text = "The lease expired due to network connection failure."
                Exit Select
            Case LexFloatClient.LF_E_SERVER_TIME
                Me.statusLabel.Text = "The lease expired because Server System time was modified."
                Exit Select
            Case LexFloatClient.LF_E_TIME
                Me.statusLabel.Text = "The lease expired because Client System time was modified."
                Exit Select
            Case Else
                Me.statusLabel.Text = "The lease expired due to some other reason."
                Exit Select
        End Select
    End Sub
```

#### Dropping License Lease

When your user is done using the app, the app should send a request to free the license, thereby making it available for other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```c

 Private Sub dropBtn_Click(sender As Object, e As EventArgs) Handles dropBtn.Click
        Dim status As Integer
        status = floatClient.DropLicense()
        If status <> LexFloatClient.LF_OK Then
            Me.statusLabel.Text = "Error Dropping License: " + status.ToString()
    	Else
    		Me.statusLabel.Text = "License dropped successfully!"
    	End If
        LexFloatClient.GlobalCleanUp()
    End Sub
```

The above code should be executed everytime user closes the app.

### Need more help?

In case you need more help for adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our[support forum](https://cryptlex.com/forums)or can contact us through[email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

