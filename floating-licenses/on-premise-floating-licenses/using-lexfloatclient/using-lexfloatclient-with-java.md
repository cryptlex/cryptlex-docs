# Using LexFloatClient with Java

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-java/tree/master/examples)

The product id is the identifier of your product that is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding the library to your app

LexFloatClient wrapper for Java is available on the [central maven repository](https://search.maven.org/artifact/com.cryptlex.lexfloatclient/lexfloatclient) and can be easily installed using maven by adding the following dependency in your POM file:

```markup
<dependency>
  <groupId>com.cryptlex.lexfloatclient</groupId>
  <artifactId>lexfloatclient</artifactId>
  <!-- Make sure that you use the latest version -->
  <version>4.5.4</version>
</dependency>
```

Alternatively, you can also download the [JAR](https://repo1.maven.org/maven2/com/cryptlex/lexfloatclient/lexfloatclient/) file and add it to your project.

LexFloatClient has a dependency on `VS2015` runtime on **Windows**. On the target machines where you will deploy your app, you can install the `VS2015` runtime, if not present, using the link: [https://www.microsoft.com/en-in/download/details.aspx?id=48145](https://www.microsoft.com/en-in/download/details.aspx?id=48145)

### Setting product id

The first LexFloatClient API function you need to use in your code is `SetHostProductId()`. It sets the product id of the product you will be adding licensing to. 

```java
LexFloatClient.SetHostProductId("PASTE_PRODUCT_ID");
```

### Requesting license lease

To receive a floating license, you will use `SetHostUrl()`, `SetFloatingLicenseCallback()` and `RequestFloatingLicense()`LexFloatClient API methods. It sets the LexFloatServer address, the callback for status notifications, contacts the server and receives the floating license.

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

License lease automatically renews itself in a background thread. When a license is renewed or it fails to renew, the callback is invoked \(from the background thread\).

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

In case you need more help with adding LexFloatClient to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

