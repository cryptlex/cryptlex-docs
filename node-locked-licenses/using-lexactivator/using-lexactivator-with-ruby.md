# Using LexActivator with Ruby

First of all, login to your Cryptlex account and download LexActivator library for Windows, MacOS or Linux:

* ​[Download LexActivator for Windows](https://app.cryptlex.com/downloads)​
* ​[Download LexActivator for MacOS](https://app.cryptlex.com/downloads)
* ​[Download LexActivator for Linux](https://app.cryptlex.com/downloads)​

The above download package contains the library which you will be using to add licensing to your app.

## Adding licensing to your app <a id="adding-licensing-to-your-app"></a>

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the Product.dat for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-ruby).

Product.dat contains product data which is used by LexActivator. Product id is the identifier of your product which is to be used in the code.

### Adding library to your app <a id="adding-library-to-your-app"></a>

LexActivator example project for Ruby contains **LexActivator.rb** and **LexStatusCodes.rb** files. You will need to add these files to your Ruby project. It contains all the LexActivator API functions needed to add licensing to your app.

### Setting product.dat file and product Id <a id="setting-product.dat-file-and-product-id"></a>

The first thing you need to do is either embed the Product.dat file in your app using `SetProductData()` function or set the absolute path of the file using `SetProductFile()` function.

The next thing you need to do is to set the product id of your application in your code using `SetProductId()` function. It sets the id of the product you will be adding licensing to.

```ruby
LexActivator.SetProductData(LexActivator::encode_utf16("PASTE_CONTENT_OF_PRODUCT.DAT_FILE"));
LexActivator.SetProductId(LexActivator::encode_utf16("PASTE_PRODUCT_ID"), LexActivator::PermissionFlags::LA_USER);
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing   `PermissionFlags::LA_USER` flag, you need to pass `PermissionFlags::LA_SYSTEM` flag.

### License activation <a id="license-activation"></a>

To activate the license in your app using the license key, you will use `ActivateLicense()` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```ruby
def activate()
  status = LexActivator.SetLicenseKey(LexActivator::encode_utf16("PASTE_LICENSE_KEY"))
  if LexStatusCodes::LA_OK != status
    puts "Error Code: #{status}"
    exit(status)
  end

  status = LexActivator.SetActivationMetadata(LexActivator::encode_utf16("key1"), LexActivator::encode_utf16("value1"))
  if LexStatusCodes::LA_OK != status
    puts "Error Code: #{status}"
    exit(status)
  end

  status = LexActivator.ActivateLicense()
  if LexStatusCodes::LA_OK == status || LexStatusCodes::LA_EXPIRED == status || LexStatusCodes::LA_SUSPENDED == status
    puts "License activated successfully: #{status}"
  else
    puts "License activation failed: #{status}"
  end
end
```

The above code should be executed at the time of license activation.

### Verifying license activation <a id="verifying-license-activation"></a>

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this you need to use `IsLicenseGenuine()` LexActivator API function.

```ruby
def main()
  status = LexActivator.SetProductData(LexActivator::encode_utf16("PASTE_CONTENT_OF_PRODUCT.DAT_FILE"))
  if LexStatusCodes::LA_OK != status
    puts "Error Code: #{status}"
    exit(status)
  end
  
  status = LexActivator.SetProductId(LexActivator::encode_utf16("PASTE_PRODUCT_ID"), LexActivator::PermissionFlags::LA_USER)
  if LexStatusCodes::LA_OK != status
    puts "Error Code: #{status}"
    exit(status)
  end
  
  status = LexActivator.IsLicenseGenuine()
  if LexStatusCodes::LA_OK == status
    puts "License is genuinely activated!"
  elsif LexStatusCodes::LA_EXPIRED == status
    puts "License is genuinely activated but has expired!"
  elsif LexStatusCodes::LA_SUSPENDED == status
    puts "License is genuinely activated but has been suspended!"
  elsif LexStatusCodes::LA_GRACE_PERIOD_OVER == status
    puts "License is genuinely activated but grace period is over!"
  else
    puts "License is not activated: #{status}";
  end
end
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread.

## Need more help <a id="need-more-help"></a>

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

