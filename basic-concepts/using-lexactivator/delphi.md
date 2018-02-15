## Using LexActivator with Delphi

First of all, login to your Cryptlex account and download LexActivator for Windows or Mac OS X:

* [Download LexActivator for Windows](https://cryptlex.com/app/api)
* [Download LexActivator for Mac OS X](https://cryptlex.com/app/api)

The above download package includes an example project. It contains all the functions you will be using to add licensing to your app.

### Adding Licensing to your App

After you've added a product for your app in the dashboard, go to the version page of the product you will be adding licensing to. You will need to do two things:

* Download the Product.dat for the product version.
* Note the Version GUID for the product version.

[![](https://cryptlex.com/public/img/docs/version.png "product-version")](https://cryptlex.com/public/img/docs/version.png)

Product.dat contains version data which is used by LexActivator and is to be included in the same directory as your app. Version GUID is the identifier of your product version which is to be used in the code.

#### Adding Library to your App

LexActivator example project for Delphi \(7 or newer\) contains the**LexActivator.pas**unit file. In addition to that it includes**LexActivator.DelphiFeatures.pas**unit file used internally.

You need to add these files to your app in order to use LexActivator API in your app. Both units must be added, but only LexActivator unit must be added to uses list.

#### Setting Version GUID

The first LexActivator API procedure you need to use in your code is`SetVersionGUID()`. It sets the version GUID of the product you will be adding licensing to. If the Product.dat file is not present in the same directory as your app or has been renamed, you need to invoke`SetProductFile()`procedure first to set the path of the product file.

The first LexActivator API function you need to use in your code is`SetVersionGUID()`. It sets the version GUID of the product you will be adding licensing to.

```c

    SetVersionGUID('YOUR VERSION GUID', lfUser);
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing`lfUser`flag, you need to pass`lfSystem`flag.

#### Online Activation

To activate your app using the product key, you will use`ActivateProduct()`LexActivator API function. It contacts the Cryptlex servers, validates the key and returns with encrypted and digitally signed response which it stores and uses to activate the product.

```c
var
      Step: string;
      Status: TLAKeyStatus;
    begin
      try
        Step := 'SetProductKey'; SetProductKey('YOUR PRODUCT KEY');
        Step := 'ActivateProduct'; Status := ActivateProduct;
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

The above code should be executed at the time of registration, ideally on a button click.

#### Verifying Activation

Each time, your app starts, you need to verify whether your app is already activated or not. This verification should occur locally by verifying the cryptographic digital signature fetched at the time of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate the activation periodically. For this you need to use`IsProductGenuine()`LexActivator API function.

```c
  var
      Step: string;
      Status: TLAKeyStatus;
    begin
      try
        Step := 'SetVersionGUID'; SetVersionGUID('YOUR VERSION GUID');
        Step := 'IsProductGenuine'; Status := IsProductGenuine;
        case Status of
          lkOK: ShowMessage('Product is genuinely activated!');
          lkExpired: ShowMessage('Product is genuinely activated, but license validity has expired!');
          lkGPOver: ShowMessage('Product is genuinely activated, but grace period is over!');
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

The above code should be executed everytime user starts the app. After verifying locally, it schedules a server check in a separate thread.

### Need more help?

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our[support forum](https://cryptlex.com/forums)or can contact us through[email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

