## Using LexFloatClient with Java

First of all, login to your Cryptlex account and download LexFloatClient for Windows, Mac OS X or Linux:

* [Download LexFloatClient for Windows](https://cryptlex.com/app/api)
* [Download LexFloatClient for Mac OS X](https://cryptlex.com/app/api)
* [Download LexFloatClient for Linux](https://cryptlex.com/app/api)

The above download package includes an example project. It contains all the functions you will be using to add licensing to your app.

### Adding Licensing to your App

After you've added a product for your app in the dashboard, go to the version page of the product you will be adding licensing to. You will need to do two things:

* Download the Product.dat for the product version.
* Note the Version GUID for the product version.

[![](https://cryptlex.com/public/img/docs/version.png "product-version")](https://cryptlex.com/public/img/docs/version.png)

Product.dat contains version data which is used by LexFloatClient and is to be included in the same directory as your app. Version GUID is the identifier of your product version which is to be used in the code.

#### Adding Library to your App

LexFloatClient example project \(Netbeans\) for Java contains the LexFloatClient package and[JNA](https://github.com/java-native-access/jna)jar file. You will need to add these files to your project. It contains all the LexFloatClient API functions needed to add licensing to your app.

LexFloatClient is compiled as a native binary, so you will need to include the LexFloatClient binaries for every platform you want to support. It looks for the native platform libraries in the folder "lexfloatclient" relative to your jar file. The folder structure should be as follows:

```c

myapp.jar
lexfloatclient/
     mac/
          libLexFloatClient.dylib
     win32-x86/
          LexFloatClient.dll
     win32-x86-64/
          LexFloatClient.dll
     linux-x86/
          libLexFloatClient.so
     linux-x86-64/
          libLexFloatClient.so


```

In case you are creating platform specific installers, you only need to include the versions of LexFloatClient applicable to that platform.

#### Setting Version GUID

The first LexFloatClient API function you need to use in your code is`SetVersionGUID()`. It sets the version GUID of the product you will be adding licensing to. If the Product.dat file is not present in the same directory as your app or has been renamed, you need to invoke`SetProductFile()`function first to set the path of the product file.

```c
   LexFloatClient floatClient = new LexFloatClient();
    floatClient.SetVersionGUID("YOUR VERSION GUID");
```



#### Requesting License Lease

To receive a floating license, you will use`SetFloatServer()`,`AddLicenseCallbackListener()`and`RequestLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for error notifications, contacts the server and receives the leased license.

```c
  try
    {
        CallbackEventListener eventListener = new CallbackEventListener();
        LexFloatClient floatClient = new LexFloatClient();
        floatClient.SetVersionGUID("YOUR VERSION GUID");
        floatClient.SetFloatServer("localhost", (short) 8090);
        floatClient.AddLicenseCallbackListener(eventListener);
        floatClient.RequestLicense();
        System.out.println("Success! License Acquired");
    } catch (LexFloatClientException ex)
    {
        System.out.println(ex.getCode() + ": " + ex.getMessage());
    }
```

The above code can be executed everytime user starts the app or needs a new license.

#### Renewing License Lease

License lease automatically renews itself in a background thread. When something goes wrong, LicenseCallback is invoked.

```c
  class CallbackEventListener implements LicenseCallbackEvent
    {
        @Override
        public void LicenseCallback(int status)
        {
            switch (status)
            {
                case LexFloatClientException.LF_E_LICENSE_EXPIRED:
                    System.out.println("The lease expired before it could be renewed.");
                    break;
                case LexFloatClientException.LF_E_LICENSE_EXPIRED_INET:
                    System.out.println("The lease expired due to network connection failure.");
                    break;
                case LexFloatClientException.LF_E_SERVER_TIME:
                    System.out.println("The lease expired because Server System time was modified.");
                    break;
                case LexFloatClientException.LF_E_TIME:
                    System.out.println("The lease expired because Client System time was modified.");
                    break;
                default:
                    System.out.println("The lease expired due to some other reason.");
                    break;
            }
        }
    }
```

You would ideally request for a new license if LicenseCallback gets invoked.

#### Dropping License Lease

When your user is done using the app, the app should send a request to free the license, thereby making it available for other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```c
 try
    {
        floatClient.DropLicense();
        System.out.println("Success! License Dropped");
        LexFloatClient.GlobalCleanUp();
    } catch (LexFloatClientException ex)
    {
        System.out.println(ex.getCode() + ": " + ex.getMessage());
    }
```

The above code should be executed everytime user closes the app.

### Need more help?

In case you need more help for adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our[support forum](https://cryptlex.com/forums)or can contact us through[email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

