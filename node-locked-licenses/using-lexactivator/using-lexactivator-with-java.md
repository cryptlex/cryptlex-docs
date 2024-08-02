# Using LexActivator with Java

## Adding licensing to your app <a href="#adding-licensing-to-your-app" id="adding-licensing-to-your-app"></a>

After you've added a product for your app in the admin portal, you will need to do the following things:

* Note the product id for the product (from the actions menu in the table).
* Download the Product.dat for the product (from the actions menu in the table).
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-java/tree/master/examples)

Product.dat contains product data that is used by LexActivator. The product id is the identifier of your product that is to be used in the code.

### Adding the library to your app <a href="#adding-library-to-your-app" id="adding-library-to-your-app"></a>

LexActivator wrapper for Java is available on the [central maven repository](https://search.maven.org/artifact/com.cryptlex.lexactivator/lexactivator) and can be easily installed using maven by adding the following dependency in your POM file:

```markup
<dependency>
  <groupId>com.cryptlex.lexactivator</groupId>
  <artifactId>lexactivator</artifactId>
  <!-- Make sure that you use the latest version -->
  <version>3.14.9</version>
</dependency>
```

Alternatively, you can also download the [JAR](https://repo1.maven.org/maven2/com/cryptlex/lexactivator/lexactivator/) file and add it to your project.

LexActivator has a dependency on `VS2015` runtime on **Windows**. On the target machines where you will deploy your app, you can install the `VS2015` runtime, if not present, using the link: [https://www.microsoft.com/en-in/download/details.aspx?id=48145](https://www.microsoft.com/en-in/download/details.aspx?id=48145)

### Setting product.dat file and product Id <a href="#setting-product.dat-file-and-product-id" id="setting-product.dat-file-and-product-id"></a>

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```java
LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
LexActivator.SetProductId("PASTE_PRODUCT_ID", LA_USER);
```

If your app requires admin (root) privileges to run (e.g. services, daemons etc.), instead of passing `LA_USER` flag, you need to pass `LA_SYSTEM` flag.

{% hint style="info" %}
In case your app doesn't have write access to the disk, you can use `LA_IN_MEMORY` flag instead, which causes all the data to be stored in the memory. But this would require you to activate the license every time you restart the app.
{% endhint %}

### License activation <a href="#license-activation" id="license-activation"></a>

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```csharp
int status;
try
{
    LexActivator.SetLicenseKey("PASTE_LICENSE_KEY");
    LexActivator.SetActivationMetadata("key1", "value1");
    status = LexActivator.ActivateLicense();
    if (LexActivator.LA_OK == status || LexActivator.LA_EXPIRED == status || LexActivator.LA_SUSPENDED == status)
    {
        System.out.println("License activated successfully: " + status);
    } 
    else
    {
        System.out.println("License activation failed: " + status);
    }
} 
catch (LexActivatorException ex)
{
    System.out.println(ex.getCode() + ": " + ex.getMessage());
}
```

The above code should be executed at the time of registration, ideally on a button click.

### Verifying license activation <a href="#verifying-license-activation" id="verifying-license-activation"></a>

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this, you need to use `IsLicenseGenuine()` LexActivator API function.

```java
int status;
try
{
    LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");    
    LexActivator.SetProductId("PASTE_PRODUCT_ID", LexActivator.LA_USER);
    status = LexActivator.IsLicenseGenuine();
    if (LexActivator.LA_OK == status)
    {
        System.out.println("License is genuinely activated!");
    } 
    else if (LexActivator.LA_EXPIRED == status)
    {
        System.out.println("License is genuinely activated but has expired!");
    } 
    else if (LexActivator.LA_GRACE_PERIOD_OVER == status)
    {
        System.out.println("License is genuinely activated but grace period is over!");
    } 
    else if (LexActivator.LA_SUSPENDED == status)
    {
        System.out.println("License is genuinely activated but has been suspended!");
    } 
    else
    {
    	System.out.println("License is not activated: " + status);
    }
} catch (LexActivatorException ex)
{
    System.out.println(ex.getCode() + ": " + ex.getMessage());
}
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help <a href="#need-more-help" id="need-more-help"></a>

In case you need more help with adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).
