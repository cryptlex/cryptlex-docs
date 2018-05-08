# Using LexFloatClient with Java

First of all, login to your Cryptlex account and download LexFloatClient library for Windows, MacOS or Linux:

* [Download LexFloatClient for Windows](https://app.cryptlex.com/downloads)
* [Download LexFloatClient for MacOS](https://app.cryptlex.com/downloads)
* [Download LexFloatClient for Linux](https://app.cryptlex.com/downloads)

The above download package contains the library which you will be using to add licensing to your app.

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-java)

Product id is the identifier of your product which is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding library to your app

LexFloatClient example project \(Netbeans\) for Java contains the LexFloatClient package and [JNA](https://github.com/java-native-access/jna) jar file. You will need to add these files to your project. It contains all the LexFloatClient API functions needed to add licensing to your app.

LexFloatClient is compiled as a native binary, so you will need to include the LexFloatClient binaries for every platform you want to support. It looks for the native platform libraries in the folder "lexfloatclient" relative to your jar file. The folder structure should be as follows:

```text
myapp.jar
lexactivator/
     mac/
          libLexFloatClient.dylib
     win32-x86/
          libLexFloatClient.dll
     win32-x86-64/
          libLexFloatClient.dll
     linux-x86/
          libLexFloatClient.so
     linux-x86-64/
          libLexFloatClient.so
```

In case you are creating platform specific installers, you only need to include the versions of LexFloatClient applicable to that platform.

### Setting product id

The first LexFloatClient API function you need to use in your code is `SetProductId()`. It sets the product id of the product you will be adding licensing to. 

```csharp
LexFloatClient floatClient = new LexFloatClient();
floatClient.SetProductId("PASTE_PRODUCT_ID");
```

### Requesting license lease

To receive a floating license, you will use `SetFloatServer()`, `SetLicenseCallback()` and `RequestLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for status notifications, contacts the server and receives the leased license.

```java
try
{
    CallbackEventListener eventListener = new CallbackEventListener();
    LexFloatClient floatClient = new LexFloatClient();
    floatClient.SetProductId("PASTE_PRODUCT_ID");
    floatClient.SetFloatServer("localhost", (short) 8090);
    floatClient.AddLicenseCallbackListener(eventListener);
    floatClient.RequestLicense();
    System.out.println("Success! License Acquired");
} catch (LexFloatClientException ex)
{
    System.out.println(ex.getCode() + ": " + ex.getMessage());
}
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing license lease

License lease automatically renews itself in a background thread. When something goes wrong, Callback is invoked \(from background thread\).

```java
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

You would usually request for a new license if callback gets invoked.

### Dropping license lease

When your user is done using the app, the app should send a request to free the license, thereby making it available for other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```java
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

The above code should be executed every time user closes the app.

## Need more help

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://cryptlex.com/forums) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

