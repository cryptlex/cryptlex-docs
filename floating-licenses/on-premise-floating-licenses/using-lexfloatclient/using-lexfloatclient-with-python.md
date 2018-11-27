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

The first LexFloatClient API function you need to use in your code is `GetHandle()`. It sets the product id of the product you will be adding licensing to. 

```cpp
handle = ctypes.c_uint()
status = LexFloatClient.GetHandle("PASTE_PRODUCT_ID", ctypes.byref(handle))
```

### Requesting license lease

To receive a floating license, you will use `SetFloatServer()`, `SetLicenseCallback()` and `RequestLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for status notifications, contacts the server and receives the leased license.

```python
handle = ctypes.c_uint()
status = LexFloatClient.GetHandle("PASTE_PRODUCT_ID", ctypes.byref(handle))
if LexFloatClient.StatusCodes.LF_OK != status:
    # handle error
status = LexFloatClient.SetFloatServer(handle.value, "localhost", 8090)
if LexFloatClient.StatusCodes.LF_OK != status:
    # handle error
status = LexFloatClient.SetLicenseCallback(handle.value, licence_callback_fn)
if LexFloatClient.StatusCodes.LF_OK != status:
    # handle error
status = LexFloatClient.RequestLicense(handle.value)
if LexFloatClient.StatusCodes.LF_OK != status:
    # handle error
print("License leased successfully!")
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing license lease

License lease automatically renews itself in a background thread. When something goes wrong, Callback is invoked \(from background thread\).

```python
def licence_callback(status):
    if LexFloatClient.StatusCodes.LF_E_LICENSE_EXPIRED == status:
        print("The lease expired before it could be renewed.")
    elif LexFloatClient.StatusCodes.LF_E_LICENSE_EXPIRED_INET == status:
        print("The lease expired due to network connection failure.")
    elif LexFloatClient.StatusCodes.LF_E_SERVER_TIME == status:
        print("The lease expired because Server System time was modified.")
    elif LexFloatClient.StatusCodes.LF_E_TIME == status:
        print("The lease expired because Client System time was modified.")
    else:
        print("The lease expired due to some other reason: ", status)

```

You would usually request for a new license if Callback gets invoked.

### Dropping license lease

When your user is done using the app, the app should send a request to free the license, thereby making it available for other users. If the app doesn't, the license becomes useless \(zombie\) until lease time is over.

```python
if LexFloatClient.StatusCodes.LF_OK != status:
    # handle error
print("Success! License dropped.")
LexFloatClient.GlobalCleanUp()
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

