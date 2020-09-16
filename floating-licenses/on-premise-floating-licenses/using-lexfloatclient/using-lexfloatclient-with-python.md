# Using LexFloatClient with Python

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-python/tree/master/examples)

Product id is the identifier of your product which is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding library to your app

LexFloatClient wrapper for Python can be easily installed through [pip](https://pypi.org/project/cryptlex.lexfloatclient/):

```bash
pip install cryptlex.lexfloatclient
```

LexFloatClient has a dependency on `VS2015` runtime on **Windows**. On the target machines where you will deploy your app, you can install the `VS2015` runtime, if not present, using the link: [https://www.microsoft.com/en-in/download/details.aspx?id=48145](https://www.microsoft.com/en-in/download/details.aspx?id=48145)

LexFloatClient has a dependency on `libnss3` library on **Linux**. On the target machines where you will deploy your app, ensure `libnss3` library is installed.

### Setting product id

The first LexFloatClient API function you need to use in your code is `SetHostProductId()`. It sets the product id of the product you will be adding licensing to. 

```python
LexFloatClient.SetHostProductId("PASTE_PRODUCT_ID");
```

### Requesting floating license

To receive a floating license, you will use `SetHostUrl()`, `SetFloatingLicenseCallback()` and `RequestFloatingLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for status notifications, contacts the server and receives the floating license.

```python
def main():
    try:
        LexFloatClient.SetHostProductId("PASTE_PRODUCT_ID")
        LexFloatClient.SetHostUrl("http://localhost:8090")
        LexFloatClient.SetFloatingLicenseCallback(licence_callback_fn)
        LexFloatClient.RequestFloatingLicense()
        print("Success! License acquired.)
    except LexFloatClientException as exception:
        print('Error code:', exception.code, exception.message)
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing floating license

License lease automatically renews itself in a background thread. When license is renewed or it fails to renew, Callback is invoked \(from background thread\).

```python
def licence_callback_fn(status):
    if LexFloatStatusCodes.LF_OK == status:
        print("The license lease has renewed successfully.")
    elif LexFloatStatusCodes.LF_E_LICENSE_NOT_FOUND == status:
        print("The license expired before it could be renewed.")
    elif LexFloatStatusCodes.LF_E_LICENSE_EXPIRED_INET == status:
        print("The license expired due to network connection failure.")
    else:
        print("The license renew failed due to other reason. Error code: ", status)
```

### Dropping floating license

When your user is done using the app, the app should send a request to free the license, thereby making it available to other users. If the app doesn't, the license becomes useless \(zombie\) until lease time is over.

```python
LexFloatClient.DropFloatingLicense()
print("Success! License dropped.")
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help for adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

