# Using LexActivator with Java

## Using LexActivator with C, C++ & Objective C

First of all, login to your Cryptlex account and download LexActivator library for Windows, Mac OS X or Linux:

* ​[Download LexActivator for Windows](https://cryptlex.com/app/api)​
* ​[Download LexActivator for Mac OS X](https://cryptlex.com/app/api)​
* ​[Download LexActivator for Linux](https://cryptlex.com/app/api)​

The above download package contains the library  which you will be using to add licensing to your app.

## Adding Licensing to your App {#adding-licensing-to-your-app}

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the Product.dat for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-java)

Product.dat contains product data which is used by LexActivator. Product id is the identifier of your product which is to be used in the code.

### Adding Library to your App {#adding-library-to-your-app}

LexActivator example project \(Netbeans\) for Java contains the LexActivator package and [JNA](https://github.com/java-native-access/jna) jar file. You will need to add these files to your project. It contains all the LexActivator API functions needed to add licensing to your app.

LexActivator is compiled as a native binary, so you will need to include the LexActivator binaries for every platform you want to support. It looks for the native platform libraries in the folder "lexactivator" relative to your jar file. The folder structure should be as follows:

```text
myapp.jar
lexactivator/
     mac/
          libLexActivator.dylib
     win32-x86/
          LexActivator.dll
     win32-x86-64/
          LexActivator.dll
     linux-x86/
          libLexActivator.so
     linux-x86-64/
          libLexActivator.so
```

In case you are creating platform specific installers, you only need to include the versions of LexActivator applicable to that platform.

### Setting Product.dat file and Product Id {#setting-product.dat-file-and-product-id}

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```java
LexActivator.SetProductData("PASTE_CONTENT_OF_PRODUCT.DAT_FILE");
LexActivator.SetProductId("PASTE_PRODUCT_ID", LA_USER);
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing `LA_USER` flag, you need to pass `LA_SYSTEM` flag.

### License Activation {#license-activation}

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```csharp
int status;
try
{
    LexActivator.SetLicenseKey("PASTE_LICENSE_KEY");
    LexActivator.SetActivationMetadata("key1", "value1");
    status = LexActivator.ActivateLicense();
    if (LexActivator.LA_OK == status || LexActivator.LA_EXPIRED == status || LexActivator.LA_SUSPENDED == status || LexActivator.LA_USAGE_LIMIT_REACHED == status)
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

### Verifying License Activation {#verifying-license-activation}

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this you need to use `IsLicenseGenuine()` LexActivator API function.

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
    else if (LexActivator.LA_USAGE_LIMIT_REACHED == status)
    {
        System.out.println("License is genuinely activated but has reached it's usage limit!");
    } 
    else
    {
    	System.out.println("License is not activated!");
    }
} catch (LexActivatorException ex)
{
    System.out.println(ex.getCode() + ": " + ex.getMessage());
}
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need More Help {#need-more-help}

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://cryptlex.com/forums) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

