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

The first LexFloatClient API function you need to use in your code is `SetHostProductId()`. It sets the product id of the product you will be adding licensing to. 

```java
LexFloatClient.SetHostProductId("PASTE_PRODUCT_ID");
```

### Requesting license lease

To receive a floating license, you will use `SetHostUrl()`, `SetFloatingLicenseCallback()` and `RequestFloatingLicense()`LexFloatClient API methods. It sets LexFloatServer address, callback for status notifications, contacts the server and receives the floating license.

```java
try {
    CallbackEventListener eventListener = new CallbackEventListener();
    LexFloatClient.SetHostProductId("PASTE_PRODUCT_ID");
    LexFloatClient.SetHostUrl("http://localhost:8090");
    LexFloatClient.AddLicenseCallbackListener(eventListener);

    LexFloatClient.RequestFloatingLicense();
    System.out.println("Success! License acquired.");
} catch (LexFloatClientException ex) {
    System.out.println(ex.getCode() + ": " + ex.getMessage());
} catch (IOException ex) {
    System.out.println(ex.getMessage());
}
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing floating license

License lease automatically renews itself in a background thread. When license is renewed or it fails to renew, Callback is invoked \(from background thread\).

```java
class CallbackEventListener implements LicenseCallbackEvent {
    @Override
    public void LicenseCallback(int status) {
        switch (status) {
        case LexFloatClient.LF_OK:
            System.out.println("The license lease has renewed successfully.");
            break;
        case LexFloatClientException.LF_E_LICENSE_NOT_FOUND:
            System.out.println("The license expired before it could be renewed.");
            break;
        case LexFloatClientException.LF_E_LICENSE_EXPIRED_INET:
            System.out.println("The license expired due to network connection failure.");
            break;
        default:
            System.out.println("The license renew failed due to other reason. Error code: " + Integer.toString(status));
            break;
        }
    }
}
```

### Dropping floating license

When your user is done using the app, the app should send a request to free the license, thereby making it available to other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```java
try {
    LexFloatClient.DropFloatingLicense();
    System.out.println("Success! License dropped successfully.");
} catch (LexFloatClientException ex) {
    System.out.println(ex.getCode() + ": " + ex.getMessage());
}
```

The above code should be executed every time user closes the app.

## Need more help

In case you need more help for adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

