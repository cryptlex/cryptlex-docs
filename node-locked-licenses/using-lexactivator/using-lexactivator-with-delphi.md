# Using LexActivator with Delphi

First of all, login to your Cryptlex account and download the LexActivator library for Windows or macOS:

* ​[Download LexActivator for Windows](https://app.cryptlex.com/downloads)​
* ​[Download LexActivator for macOS](https://app.cryptlex.com/downloads)​

The above download package contains the library which you will be using to add licensing to your app.

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the Product.dat for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexactivator-delphi)

Product.dat contains product data that is used by LexActivator. The product id is the identifier of your product that is to be used in the code.

### Adding the library to your app

LexActivator example project for Delphi \(7 or newer\) contains the **LexActivator.pas** unit file. In addition to that, it includes **LexActivator.DelphiFeatures.pas** unit file used internally.

You need to add these files to your app in order to use LexActivator API in your app. Both units must be added, but only the LexActivator unit must be added to the uses list. Depending on the OS you are targeting you need to copy the respective LexActivator.dll, libLexActivator.so, or libLexActivator.dylib to your project.

LexActivator has a dependency on `VS2015` runtime on **Windows**. On the target machines where you will deploy your app, you can install the `VS2015` runtime, if not present, using the link: [https://www.microsoft.com/en-in/download/details.aspx?id=48145](https://www.microsoft.com/en-in/download/details.aspx?id=48145)

### Setting product.dat file and product Id

The first thing you need to do is either embed the Product.dat file in your app using `LexActivator.SetProductData` function or set the absolute path of the file using `LexActivator.SetProductFile` function.

The next thing you need to do is to set the product id of your application in your code using `LexActivator.SetProductId` function. It sets the id of the product you will be adding licensing to.

```c
SetProductData('PASTE_CONTENT_OF_PRODUCT.DAT_FILE');
SetProductId('PASTE_PRODUCT_ID', lfUser);
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing `lfUser` flag, you need to pass `lfSystem` flag.

{% hint style="info" %}
In case your app doesn't have write access to the disk, you can use `lfInMemory` flag instead, which causes all the data to be stored in the memory. But this would require you to activate the license every time you restart the app.
{% endhint %}

### License activation

To activate the license in your app using the license key, you will use `LexActivator.ActivateLicense` LexActivator API function. It invokes the `/v3/activations` Cryptlex Web API endpoint, verifies the encrypted and digitally signed response to validate the license.

```c
var
  Step: string;
  Status: TLAKeyStatus;
begin
  try
    Step := 'SetLicenseKey'; SetLicenseKey('PASTE_LICENSE_KEY');
    Step := 'ActivateLicense'; Status := ActivateLicense;
    case Status of
      lkOK: ShowMessage('Activation successful!');
      lkExpired: ShowMessage('Activation successful, but license validity has expired!');
    else
      ShowMessage('Error activating the product: ' + LAKeyStatusToString(Status));
    end;
  except
    on E: Exception do
    begin
      ShowMessage('Exception from ' + Step + ': ' + E.ClassName + ': ' + E.Message);
    end;
  end;
end;
```

The above code should be executed at the time of license activation, ideally on a button click.

### Verifying license activation

Each time, your app starts, you need to verify whether your license is already activated or not. This verification should occur locally by verifying the cryptographic digital signature of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate and sync the license activation periodically. For this, you need to use `LexActivator.IsLicenseGenuine` LexActivator API function.

```c
var
  Step: string;
  Status: TLAKeyStatus;
begin
  try
    Step := 'SetProductData'; SetProductData('PASTE_CONTENT_OF_PRODUCT.DAT_FILE');
    Step := 'SetProductId'; SetProductId('PASTE_PRODUCT_ID', lfUser);
    Step := 'IsLicenseGenuine'; Status := IsLicenseGenuine;
    case Status of
      lkOK: ShowMessage('License is genuinely activated!');
      lkExpired: ShowMessage('License is genuinely activated, but has validity has expired!');
      lkGracePeriodOver: ShowMessage('License is genuinely activated, but grace period is over!');
    else
      ShowMessage('Error code: ' + LAKeyStatusToString(Status));
    end;
  except
    on E: Exception do
    begin
      ShowMessage('Exception from ' + Step + ': ' + E.ClassName + ': ' + E.Message);
    end;
  end;
end;
```

The above code should be executed every time user starts the app. After verifying locally, it schedules a periodic server check in a separate thread. `LexActivator.SetLicenseCallback` can be used to set notification callback.

## Need more help

In case you need more help with adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://forums.cryptlex.com) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

