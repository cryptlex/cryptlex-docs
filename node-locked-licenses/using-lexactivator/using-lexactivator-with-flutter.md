# Using LexActivator with Flutter

## Adding licensing to your app

After you've added a product for your app in the admin portal, you will need to do the following things:

* Note the product id for the product (from the actions menu in the table).
* Download the Product.dat for the product (from the actions menu in the table).
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-dart).

Product.dat contains product data that is used by LexActivator. The product id is the identifier of your product that is to be used in the code.

### Adding the library to your app

LexActivator wrapper for **Dart** can be easily installed using **Flutter's package manager**:

```dart
flutter pub add lexactivator
```

{% hint style="info" %}
**LexActivator** requires the Microsoft Visual C++ 2015 (or later) Runtime on older Windows versions such as Windows 7, 8, or Server 2008/2012. If not already installed, install it from the official [Visual C++ Redistributable](https://www.microsoft.com/en-in/download/details.aspx?id=48145) or include the required DLLs with your installer.
{% endhint %}

### **Setting product.dat file and product Id**

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```dart
void initializeLexActivator() {
  LexActivator.SetProductData(productData: "PASTE_CONTENT_OF_PRODUCT.DAT_FILE");

  LexActivator.SetProductId(
      productId: "PASTE_PRODUCT_ID", flags: LexActivator.LA_USER);
}
```

If your app requires admin (root) privileges to run (e.g. services, daemons etc.), instead of passing `PermissionFlags.LA_USER` flag, you need to pass `PermissionFlags.LA_SYSTEM` flag.

If your app requires a single activation to be shared across all OS users (system-wide activation), pass the `PermissionFlags.LA_ALL_USERS` flag before activation. This flag is compatible with Windows OS only.

{% hint style="info" %}
In case your app doesn't have write access to the disk, you can use `PermissionFlags.LA_IN_MEMORY` flag instead, which causes all the data to be stored in the memory. But this would require you to activate the license every time you restart the app.
{% endhint %}

### **License activation**

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```dart
void activateLicense() {
  try {
    LexActivator.SetLicenseKey(licenseKey: 'PASTE_LICENSE_KEY');
    LexActivator.SetActivationMetadata(key: 'Metadata 1', value: 'Value 1');
    final status = LexActivator.ActivateLicense();
    
    switch (status) {
      case LexStatusCodes.LA_OK:
        print('License activated successfully!');
        break;
      case LexStatusCodes.LA_EXPIRED:
        print('License activated successfully but has expired!');
        break;
      case LexStatusCodes.LA_SUSPENDED:
        print('License activated successfully but has been suspended!');
        break;
    }
  } on LexActivatorException catch (e) {
    print('License activated failed: $e');
  }
}
 
```

The above code should be executed at the time of license activation.

### **Verifying license activation**

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this you need to use `IsLicenseGenuine()` LexActivator API function.

```dart
void main() {
  try {
    LexActivator.SetProductData(productData: 'PASTE_PRODUCT_DATA');
    LexActivator.SetProductId(productId: 'PASTE_PRODUCT_ID', flags: LexActivator.LA_USER);
    LexActivator.SetReleaseVersion(releaseVersion: 'PASTE_YOUR_RELEASE_VERSION');
    
    final status = LexActivator.IsLicenseGenuine();
    switch (status) {
      case LexStatusCodes.LA_OK:
        print('License is genuinely activated!');
        break;
      case LexStatusCodes.LA_EXPIRED:
        print('License is genuinely activated but has expired!');
        break;
      case LexStatusCodes.LA_SUSPENDED:
        print('License is genuinely activated but has been suspended!');
        break;
      case LexStatusCodes.LA_GRACE_PERIOD_OVER:
        print('License is genuinely activated but grace period is over!');
        break;
      default:
        print('License is not activated');
    }
  } on LexActivatorException catch (e) {
    print('Error: $e');
  }
}
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

### **Limitations**

The application you are building with the plugin will only build for the host architecture on Linux and Windows i.e. if you are building your application on a Linux x64, it will build for Linux x64 and not for Linux ARM.

### **Need more help**

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).
