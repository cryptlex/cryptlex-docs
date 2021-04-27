# Using LexFloatClient with Go

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-go/tree/main/examples)

The product id is the identifier of your product that is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding the library to your app

LexFloatClient wrapper for Go can be easily installed using the **go get** command:

```bash
go get -u github.com/cryptlex/lexfloatclient-go
```

**Note:** In case you are using Windows, execute the following command after installation:

```text
xcopy %USERPROFILE%\go\src\github.com\cryptlex\lexfloatclient-go\libs\windows_amd64\LexFloatClient.dll
```

This would copy the LexFloatClient.dll to your project directory.

LexFloatClient has a dependency on `VS2015` runtime on **Windows**. On the target machines where you will deploy your app, you can install the `VS2015` runtime, if not present, using the link: [https://www.microsoft.com/en-in/download/details.aspx?id=48145](https://www.microsoft.com/en-in/download/details.aspx?id=48145)

### Setting product id

The first LexFloatClient API function you need to use in your code is `SetHostProductId()`. It sets the product id of the product you will be adding licensing to. 

```python
lexfloatclient.SetHostProductId("PASTE_PRODUCT_ID");
```

### Requesting floating license

To receive a floating license, you will use `SetHostUrl()`, `SetFloatingLicenseCallback()` and `RequestFloatingLicense()`LexFloatClient API methods. It sets the LexFloatServer address, the callback for status notifications, contacts the server and receives the floating license.

```python
func main() {
	var status int
	status = lexfloatclient.SetHostProductId("PASTE_PRODUCT_ID")
	if lexfloatclient.LF_OK != status {
		fmt.Println("Error Code:", status)
		os.Exit(1)
	}
	status = lexfloatclient.SetHostUrl("http://localhost:8090")
	if lexfloatclient.LF_OK != status {
		fmt.Println("Error Code:", status)
		os.Exit(1)
	}
	lexfloatclient.SetFloatingLicenseCallback(licenseCallback)
	status = lexfloatclient.RequestFloatingLicense()
	if lexfloatclient.LF_OK != status {
		fmt.Println("Error Code:", status)
		os.Exit(1)
	}  
	fmt.Println("Success! License acquired.") 
}
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing floating license

License lease automatically renews itself in a background thread. When a license is renewed or fails to renew, the callback is invoked \(from the background thread\).

```python
func licenseCallback(status int) {
	if status == lexfloatclient.LF_OK {
		fmt.Println("The license lease has renewed successfully.")
	} else if status == lexfloatclient.LF_E_LICENSE_NOT_FOUND {
		fmt.Println("he license expired before it could be renewed.")
	} else if status == lexfloatclient.LF_E_LICENSE_EXPIRED_INET {
		fmt.Println("The license expired due to network connection failure.")
	} else {
		fmt.Println("The license renew failed due to other reason. Error code:", status)
	}
}
```

### Dropping floating license

When your user is done using the app, the app should send a request to free the license, thereby making it available to other users. If the app doesn't, the license becomes useless \(zombie\) until lease time is over.

```python
lexfloatclient.DropFloatingLicense()
fmt.Println("Success! License dropped.")
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help with adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

