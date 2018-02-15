## Using LexActivator with Java

First of all, login to your Cryptlex account and download LexActivator for Windows, Mac OS X or Linux:

* [Download LexActivator for Windows](https://cryptlex.com/app/api)
* [Download LexActivator for Mac OS X](https://cryptlex.com/app/api)
* [Download LexActivator for Linux](https://cryptlex.com/app/api)

The above download package includes an example project. It contains all the functions you will be using to add licensing to your app.

### Adding Licensing to your App

After you've added a product for your app in the dashboard, go to the version page of the product you will be adding licensing to. You will need to do two things:

* Download the Product.dat for the product version.
* Note the Version GUID for the product version.

[![](https://cryptlex.com/public/img/docs/version.png "product-version")](https://cryptlex.com/public/img/docs/version.png)

Product.dat contains version data which is used by LexActivator and is to be included in the same directory as your app. Version GUID is the identifier of your product version which is to be used in the code.

#### Adding Library to your App

LexActivator example project \(Netbeans\) for Java contains the LexActivator package and[JNA](https://github.com/java-native-access/jna)jar file. You will need to add these files to your project. It contains all the LexActivator API functions needed to add licensing to your app.

LexActivator is compiled as a native binary, so you will need to include the LexActivator binaries for every platform you want to support. It looks for the native platform libraries in the folder "lexactivator" relative to your jar file. The folder structure should be as follows:

```

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

#### Setting Version GUID

The first LexActivator API function you need to use in your code is`SetVersionGUID()`. It sets the version GUID of the product you will be adding licensing to. If the Product.dat file is not present in the same directory as your app or has been renamed, you need to invoke`SetProductFile()`function first to set the path of the product file.

```

    LexActivator
.
SetVersionGUID
(
"YOUR VERSION GUID"
,
 LexActivator
.
LA_USER
)
;
```

If your app requires admin \(root\) privileges to run \(e.g. services, daemons etc.\), instead of passing`LexActivator.LA_USER`flag, you need to pass`LexActivator.LA_SYSTEM`flag.

#### Online Activation

To activate your app using the product key, you will use`ActivateProduct()`LexActivator API function. It contacts the Cryptlex servers, validates the key and returns with encrypted and digitally signed response which it stores and uses to activate the product.

```
int
 status
;
try
{

    	LexActivator
.
SetProductKey
(
"YOUR PRODUCT KEY"
)
;

    	LexActivator
.
SetExtraActivationData
(
"sample data"
)
;

    	status 
=
 LexActivator
.
ActivateProduct
(
)
;
if
(
status 
==
 LexActivator
.
LA_OK
)
{

    		System
.
out
.
println
(
"Activation successful"
)
;
}
if
(
status 
==
 LexActivator
.
LA_EXPIRED
)
{

    		System
.
out
.
println
(
"Activation successful, but license validity has expired!"
)
;
}
else
{

    		System
.
out
.
println
(
"Error activating the product: "
+
 status
)
;
}
}
catch
(
LexActivatorException
 ex
)
{

    	System
.
out
.
println
(
ex
.
getCode
(
)
+
": "
+
 ex
.
getMessage
(
)
)
;
}
```

The above code should be executed at the time of registration, ideally on a button click.

#### Verifying Activation

Each time, your app starts, you need to verify whether your app is already activated or not. This verification should occur locally by verifying the cryptographic digital signature fetched at the time of activation. Ideally, it should also asynchronously contact Cryptlex servers to validate the activation periodically. For this you need to use`IsProductGenuine()`LexActivator API function.

```
int
 status
;
try
{

    	LexActivator
.
SetVersionGUID
(
"YOUR VERSION GUID"
,
 LexActivator
.
LA_USER
)
;


    	status 
=
 LexActivator
.
IsProductGenuine
(
)
;
if
(
LexActivator
.
LA_OK 
==
 status
)
{

    		System
.
out
.
println
(
"Product is genuinely activated!"
)
;
}
else
if
(
LexActivator
.
LA_EXPIRED 
==
 status
)
{

    		System
.
out
.
println
(
"Product is genuinely activated, but license validity has expired!"
)
;
}
else
if
(
LexActivator
.
LA_GP_OVER 
==
 status
)
{

    		System
.
out
.
println
(
"Product is genuinely activated, but grace period is over!"
)
;
}
else
{

    		System
.
out
.
println
(
"Product is not activated!"
)
;
}
}
catch
(
LexActivatorException
 ex
)
{

    	System
.
out
.
println
(
ex
.
getCode
(
)
+
": "
+
 ex
.
getMessage
(
)
)
;
}
```

The above code should be executed everytime user starts the app. After verifying locally, it schedules a server check in a separate thread.

### Need more help?

In case you need more help for adding LexActivator to your app, we'll be glad to help you make the integration. You can either post your questions on our[support forum](https://cryptlex.com/forums)or can contact us through[email](mailto:support@cryptlex.com?Subject=Using%20LexActivator).

