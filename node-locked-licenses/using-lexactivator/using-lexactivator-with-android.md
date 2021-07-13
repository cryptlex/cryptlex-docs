# Using LexActivator with Android

## Adding licensing to your app <a id="adding-licensing-to-your-app"></a>

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the Product.dat for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-android/tree/main/examples)

Product.dat contains product data that is used by LexActivator. The product id is the identifier of your product that is to be used in the code.

### Adding the library to your app <a id="adding-library-to-your-app"></a>

LexActivator wrapper for Android is available on the [central maven repository](https://search.maven.org/artifact/com.cryptlex.lexactivator/lexactivator) and can be easily installed using Gradle by adding the following dependency in your build.gradle file:

```markup
dependencies {
    implementation 'com.cryptlex.android.lexactivator:lexactivator:3.14.0'
}
```

Alternatively, you can also download the [AAR](https://repo1.maven.org/maven2/com/cryptlex/lexactivator/lexactivator/) file and add it to your project.

### Setting product.dat file, product id, data directory and Android id <a id="setting-product.dat-file-and-product-id"></a>

The first thing you need to do is set the data directory where LexActivator will store its data. You also need to provide the Android Id which is needed by LexActivator. 

The next thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

Next, you need to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```java
LexActivator.SetDataDirectory(getApplicationContext().getFilesDir().getAbsolutePath());
LexActivator.SetAndroidId(Secure.getString(getApplicationContext().getContentResolver(), Secure.ANDROID_ID));
LexActivator.SetProductData("PASTE_PRODUCT_DATA");
LexActivator.SetProductId("PASTE_PRODUCT_ID", LexActivator.LA_USER);
```

{% hint style="info" %}
In case your app doesn't have write access to the disk, you can use `LA_IN_MEMORY` flag instead, which causes all the data to be stored in the memory. But this would require you to activate the license every time you restart the app.
{% endhint %}

### License activation <a id="license-activation"></a>

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```csharp
try {
    LexActivator.SetLicenseKey(licenseKeyEditBox.getText().toString().trim());
    int status = LexActivator.ActivateLicense();
    if (LexActivator.LA_OK == status || LexActivator.LA_EXPIRED == status || LexActivator.LA_SUSPENDED == status) {
        statusTextView.setText("License activated successfully: " + status);
    } else {
        statusTextView.setText("License activation failed: " + status);
    }
} catch (LexActivatorException ex) {
    statusTextView.setText("License activation failed! Error code: " + ex.getCode() + " Error message: " + ex.getMessage());
}
```

The above code should be executed at the time of registration, ideally on a button click.

### Verifying license activation <a id="verifying-license-activation"></a>

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this, you need to use `IsLicenseGenuine()` LexActivator API function.

```java
try {
    LexActivator.SetDataDirectory(getApplicationContext().getFilesDir().getAbsolutePath());
    LexActivator.SetAndroidId(Secure.getString(getApplicationContext().getContentResolver(), Secure.ANDROID_ID));
    LexActivator.SetProductData("PASTE_PRODUCT_DATA");
    LexActivator.SetProductId("PASTE_PRODUCT_ID", LexActivator.LA_USER);
    
    int status = LexActivator.IsLicenseGenuine();
    if (LexActivator.LA_OK == status) {
        statusTextView.setText("License is genuinely activated!");
    } else if (LexActivator.LA_EXPIRED == status) {
        statusTextView.setText("License is genuinely activated but has expired!");
    } else if (LexActivator.LA_GRACE_PERIOD_OVER == status) {
        statusTextView.setText("License is genuinely activated but grace period is over!");
    } else if (LexActivator.LA_SUSPENDED == status) {
        statusTextView.setText("License is genuinely activated but has been suspended!");
    } else {
        statusTextView.setText("License is not activated. Error code: " + status);
    }
} catch (LexActivatorException ex) {
    statusTextView.setText("Error code: " + ex.getCode() + " Error message: " + ex.getMessage());
}
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help <a id="need-more-help"></a>

In case you need more help with adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

