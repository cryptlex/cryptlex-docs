# Using LexActivator with Go

## Adding licensing to your app <a href="#adding-licensing-to-your-app" id="adding-licensing-to-your-app"></a>

After you've added a product for your app in the admin portal, you will need to do the following things:

* Note the product id for the product (from the actions menu in the table).
* Download the Product.dat for the product (from the actions menu in the table).
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-go).

Product.dat contains product data that is used by LexActivator. The product id is the identifier of your product that is to be used in the code.

### Adding the library to your app <a href="#adding-library-to-your-app" id="adding-library-to-your-app"></a>

LexActivator wrapper for Go can be easily installed using the **go get** command:

```bash
go get -u github.com/cryptlex/lexactivator-go
```

**Note:** In case you are using Windows, execute the following command after installation:

```
xcopy %USERPROFILE%\go\src\github.com\cryptlex\lexactivator-go\libs\windows_amd64\LexActivator.dll
```

This would copy the LexActivator.dll to your project directory.

LexActivator has a dependency on `VS2015` runtime on **Windows**. On the target machines where you will deploy your app, you can install the `VS2015` runtime, if not present, using the link: [https://www.microsoft.com/en-in/download/details.aspx?id=48145](https://www.microsoft.com/en-in/download/details.aspx?id=48145)

{% hint style="info" %}
This package relies on `cgo` to interface with a C library. As a result, `cgo` must be enabled when building and using this package. Disabling `cgo` (e.g., by setting `CGO_ENABLED=0`) will result in compilation errors.
{% endhint %}

### Setting product.dat file and product Id <a href="#setting-product.dat-file-and-product-id" id="setting-product.dat-file-and-product-id"></a>

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```go
lexactivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE")
lexactivator.SetProductId("PASTE_PRODUCT_ID", lexactivator.LA_USER))
```

If your app requires admin (root) privileges to run (e.g. services, daemons etc.), instead of passing   `lexactivator.LA_USER` flag, you need to pass `lexactivator.LA_SYSTEM` flag.

{% hint style="info" %}
In case your app doesn't have write access to the disk, you can use `lexactiavtor.LA_IN_MEMORY` flag instead, which causes all the data to be stored in the memory. But this would require you to activate the license every time you restart the app.
{% endhint %}

### License activation <a href="#license-activation" id="license-activation"></a>

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```go
func activate() {
	var status int
	status = lexactivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE")
	if lexactivator.LA_OK != status {
		fmt.Println("Error Code:", status)
		os.Exit(1)
	}

	status = lexactivator.SetProductId("PASTE_PRODUCT_ID", lexactivator.LA_USER)
	if lexactivator.LA_OK != status {
		fmt.Println("Error Code:", status)
		os.Exit(1)
	}

	status = lexactivator.SetLicenseKey("PASTE_LICENSE_KEY")
	if lexactivator.LA_OK != status {
		fmt.Println("Error Code:", status)
		os.Exit(1)
	}

	status = lexactivator.ActivateLicense()
	if lexactivator.LA_OK == status || lexactivator.LA_EXPIRED == status || lexactivator.LA_SUSPENDED == status {
		fmt.Println("License activated successfully:", status)
	} else {
		fmt.Println("License activation failed:", status)
	}
}
```

The above code should be executed at the time of license activation.

### Verifying license activation <a href="#verifying-license-activation" id="verifying-license-activation"></a>

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this, you need to use `IsLicenseGenuine()` LexActivator API function.

```go
func main() {
	var status C.int
	status = lexactivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE")
	if lexactivator.LA_OK != status {
		fmt.Println("Error Code:", status)
		os.Exit(1)
	}
	
	status = lexactivator.SetProductId("PASTE_PRODUCT_ID", lexactivator.LA_USER)
	if lexactivator.LA_OK != status {
		fmt.Println("Error Code:", status)
		os.Exit(1)
	}
	
	status = lexactivator.SetAppVersion("PASTE_YOUR_APP_VERION")
	if lexactivator.LA_OK != status {
		fmt.Println("Error Code:", status)
		os.Exit(1)
	}
	
	status = lexactivator.IsLicenseGenuine()
	if lexactivator.LA_OK == status {
		fmt.Println("License is genuinely activated!")
	} else if lexactivator.LA_EXPIRED == status {
		fmt.Println("License is genuinely activated but has expired!")
	} else if lexactivator.LA_SUSPENDED == status {
		fmt.Println("License is genuinely activated but has been suspended!")
	} else if lexactivator.LA_GRACE_PERIOD_OVER == status {
		fmt.Println("License is genuinely activated but grace period is over!")
	} else {
		 fmt.Println("License is not activated:", status)
	}
}
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help <a href="#need-more-help" id="need-more-help"></a>

In case you need more help with adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://cryptlex.com/forums) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).
