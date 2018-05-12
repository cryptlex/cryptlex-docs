# Using LexFloatClient with Delphi

First of all, login to your Cryptlex account and download LexFloatClient library for Windows or MacOS:

* [Download LexFloatClient for Windows](https://app.cryptlex.com/downloads)
* [Download LexFloatClient for MacOS](https://app.cryptlex.com/downloads)

The above download package contains the library which you will be using to add licensing to your app.

## Adding licensing to your app

After you've added a product for your app in the dashboard, go to the product page of the product you will be adding licensing to. You will need to do two things:

* Note the product id for the product.
* Download the example project from [Github](https://github.com/cryptlex/lexfloatclient-delphi)

Product id is the identifier of your product which is to be used in the code. The product id of the LexFloatServer and LexFloatClient must match.

### Adding library to your app

LexFloatClient example project for Delphi \(7 or newer\) contains the **LexFloatClient.pas** unit file. In addition to that it includes **LexFloatClient.DelphiFeatures.pas** unit file used internally.

You need to add these files to your app in order to use LexFloatClient API in your app. Both units must be added, but only LexFloatClient unit must be added to uses list.

### Setting product id

The first LexFloatClient API procedure you need to use in your code is `GetHandle()`. It sets the product id of the product you will be adding licensing to.

```c
var
  Handle: ILFHandle;
begin
  Handle := GetHandle('PASTE_PRODUCT_ID"');
```

### Requesting license lease

To receive a floating license, you will use `ILFHandle.SetFloatServer()`, `ILFHandle.SetLicenseCallback()` and `ILFHandle.RequestLicense()` LexFloatClient API methods. It sets LexFloatServer address, callback for error notifications, contacts the server and receives the leased license.

```c
var
  Handle: ILFHandle;
  Step: string;
begin
  try
    Step := 'GetHandle';
    Handle := GetHandle('PASTE_PRODUCT_ID');
    Step := 'SetFloatServer'; Handle.SetFloatServer('localhost', 8090);
    Step := 'SetLicenseCallback';
    Handle.SetLicenseCallback(TSimpleCallback.Execute);
    Step := 'RequestLicense'; Handle.RequestLicense; WriteLn;
    Write('License leased successfully!')
  except
    on E: Exception do
    begin
      WriteLn;
      WriteLn('Exception from ', Step, ': ', E.ClassName);
      WriteLn(E.Message);
      raise;
    end;
  end;
end;
```

The above code can be executed every time user starts the app or needs a new license.

### Renewing license lease

License lease automatically renews itself in a background thread. When something goes wrong, Callback is invoked \(from background thread\). Callback can be either object method, class method or a closure \(also known as anonymous function\). Note that GUI applications cannot safely interact with GUI elements from a thread other than GUI one. `TThread.Synchronize()` method or another option must be used to avoid race conditions.

```c
{ callback implemented via class function }
type
  TSimpleCallback = class
    class procedure Execute(const Sender: ILFHandle;
      const Error: Exception; Event: TLFCallbackEvent);
  end;

class procedure TSimpleCallback.Execute(const Sender: ILFHandle;
  const Error: Exception; Event: TLFCallbackEvent);
begin
  WriteLn;
  WriteLn('Exception from ', LFCallbackEventToString(Event), ': ', Error.ClassName);
  WriteLn(Error.Message);
end;
```

You would ideally request for a new license if Callback gets invoked.

### Dropping license lease

When your user is done using the app, the app should send a request to free the license, thereby making it available for other users. If the app doesn't, the license becomes \(zombie\) useless until lease time is over.

```c
Handle := nil;
```

The above code should be executed every time user closes the app.

### **Automatic and manual ILFHandle reference management**

`ILFHandle` is a reference-counted object. Zombie licenses should be avoided, thus `ILFHandle` wrapper drops the license when its last reference is being released. Leaving a scope containing a local variable or destroying an object containing a field \(such as form object\) releases a reference, so in most cases `ILFHandle` will do its best to not to leave zombie licenses. Note that, however, early versions of Delphi had a bug: global variables were not finalized.

Low-level details can be manipulated by `ILFHandle.Handle` and `ILFHandle.Owned properties`. `CreateLFHandleWrapper()` can be used to create wrappers manually. `FindHandle()` API is notable because this low-level API had no good mapping in higher-level API. It returns LongWord Handle, which can be wrapped then into either not owned or owned wrapper, but this would be another wrapper, and reference counters won't sum. Another owner might invalidate the handle at any moment. `ILFHandle.SetLicenseCallback` must only be used on wrappers created by `GetHandle()`, other APIs should work without problem as soon as handle is still valid.

## Need more help

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our [support forum](https://cryptlex.com/forums) or can contact us through [email](mailto:support@cryptlex.com?Subject=Using%20LexFloatClient).

