# C, C++, and Objective-C

First of all, login to your Cryptlex account and download LexFloatClient for Windows, Mac OS X or Linux:

* [Download LexFloatClient for Windows](https://cryptlex.com/app/api)
* [Download LexFloatClient for Mac OS X](https://cryptlex.com/app/api)
* [Download LexFloatClient for Linux](https://cryptlex.com/app/api)

The above download package includes an example project. It contains all the functions you will be using to add licensing to your app.

## Adding Licensing to your App

After you've added a product for your app in the dashboard, go to the version page of the product you will be adding licensing to. You will need to do two things:

* Download the Product.dat for the product version.
* Note the Version GUID for the product version.

![product-version](https://cryptlex.com/public/img/docs/version.png)

Product.dat contains version data which is used by LexFloatClient and is to be included in the same directory as your app. Version GUID is the identifier of your product version which is to be used in the code.

### Adding Library to your App

LexFloatClient example project for C contains the**LexFloatClient.h**header file. In addition to that it includes**LexFloatClient.lib**file required in case of Windows. It contains all the LexFloatClient API functions needed to add licensing to your app.

Depending on the platform you are targeting**\(x86 or x64\)**you need to link the respective LexFloatClient.dll with your application.

### Setting Version GUID

The first LexFloatClient API function you need to use in your code is`GetHandle()`. It sets the version GUID of the product you will be adding licensing to. If the Product.dat file is not present in the same directory as your app or has been renamed, you need to invoke`SetProductFile()`function first to set the path of the product file.

```c
    uint32_t handle;
    GetHandle("YOUR VERSION GUID", &handle);
```

### Requesting License Lease

To receive a floating license, you will use`SetFloatServer()`,`SetLicenseCallback()`and`RequestLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for error notifications, contacts the server and receives the leased license.

```c
    int status;
    uint32_t handle;
    status = GetHandle(L"YOUR VERSION GUID", &handle);
    if(LF_OK != status)
    {
        printf("Error code: %d",status);
        getchar();
        return status;
    }
    status = SetFloatServer(handle, "localhost",8090);
    if(LF_OK != status)
    {
        printf("Error code: %d",status);
        getchar();
        return status;
    }
    status = SetLicenseCallback(handle, LicenceRefreshCallback);
    if(LF_OK != status)
    {
        printf("Error code: %d",status);
        getchar();
        return status;
    }
    status = RequestLicense(handle);
    if(LF_OK != status)
    {
        printf("Error code: %d",status);
        getchar();
        return status;
    }
    printf("License leased successfully!");
```

The above code can be executed everytime user starts the app or needs a new license.

### Renewing License Lease

License lease automatically renews itself in a background thread. When something goes wrong, Callback is invoked \(from background thread\).

```c
 void LF_CC LicenceRefreshCallback(uint32_t status)
    {
        switch (status)
        {
            case LF_E_LICENSE_EXPIRED:
                printf("The lease expired before it could be renewed.\n");
                break;
            case LF_E_LICENSE_EXPIRED_INET:
                printf("The lease expired due to network connection failure.\n");
                break;
            case LF_E_SERVER_TIME:
                printf("The lease expired because Server System time was modified.\n");
                break;
            case LF_E_TIME:
                printf("The lease expired because Client System time was modified.\n");
                break;
            default:
                printf("The lease expired due to some other reason.\n");
                break;
        }
    }
```

You would ideally request for a new license if Callback gets invoked.

### Dropping License Lease

When your user is done using the app, the app should send a request to free the license, thereby making it available for other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```c
  int status;
    status = DropLicense(handle);
    if(LF_OK != status) {
        printf("Error code: %d",status);
    }
    else {
        printf("Success! License dropped.");
    }
    GlobalCleanUp();
```

The above code should be executed everytime user closes the app.

## Need more help?

In case you need more help for adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our[support forum](https://cryptlex.com/forums)or can contact us through[email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

