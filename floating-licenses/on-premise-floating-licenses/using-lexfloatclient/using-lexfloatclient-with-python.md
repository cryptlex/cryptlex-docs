# Using LexFloatClient with Python

First of all, login to your Cryptlex account and download LexFloatClient library for Windows, MacOS or Linux:

* [Download LexFloatClient for Windows](https://app.cryptlex.com/downloads)
* [Download LexFloatClient for MacOS](https://app.cryptlex.com/downloads)
* [Download LexFloatClient for Linux](https://app.cryptlex.com/downloads)

The above download package contains the library which you will be using to add licensing to your app.

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-python)

Product id is the identifier of your product which is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding library to your app

LexFloatClient example project for Python contains **LexFloatClient.py** file. You will need to add this file to your Python project. It contains all the LexFloatClient API functions needed to add licensing to your app. Depending on the OS you are targeting you need to copy the respective LexFloatClient.dll, libLexFloatClient.so or libLexFloatClient.dylib to your project.

### Setting product id

The first LexFloatClient API function you need to use in your code is `SetHostProductId()`. It sets the product id of the product you will be adding licensing to. 

```python
LexFloatClient.SetHostProductId("PASTE_PRODUCT_ID");
```

### Requesting floating license

To receive a floating license, you will use `SetHostUrl()`, `SetFloatingLicenseCallback()` and `RequestFloatingLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for status notifications, contacts the server and receives the floating license.

```python
status = LexFloatClient.SetHostProductId("PASTE_PRODUCT_ID")
if LexFloatClient.StatusCodes.LF_OK != status:
    # handle error
status = LexFloatClient.SetHostUrl("http://localhost:8090")
if LexFloatClient.StatusCodes.LF_OK != status:
    # handle error
status = LexFloatClient.SetFloatingLicenseCallback(licence_callback_fn)
if LexFloatClient.StatusCodes.LF_OK != status:
    # handle error
status = LexFloatClient.RequestFloatingLicense()
if LexFloatClient.StatusCodes.LF_OK != status:
    # handle error
print("License leased successfully!")
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing floating license

License lease automatically renews itself in a background thread. When license is renewed or it fails to renew, Callback is invoked \(from background thread\).

```python
def licence_callback(status):
    if LexFloatClient.StatusCodes.LF_OK == status:
        print("The license lease has renewed successfully.")
    elif LexFloatClient.StatusCodes.LF_E_LICENSE_NOT_FOUND == status:
        print("The license expired before it could be renewed.")
    elif LexFloatClient.StatusCodes.LF_E_LICENSE_EXPIRED_INET == status:
        print("The license expired due to network connection failure.")
    else:
        print("The license renew failed due to other reason. Error code: ", status)
```

### Dropping floating license

When your user is done using the app, the app should send a request to free the license, thereby making it available to other users. If the app doesn't, the license becomes useless \(zombie\) until lease time is over.

```python
status = LexFloatClient.DropFloatingLicense()
if LexFloatClient.StatusCodes.LF_OK != status:
    # handle error
print("Success! License dropped.")
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help for adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

