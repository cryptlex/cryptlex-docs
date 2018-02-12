## Extra Activation Data

You can pass additional data to the Cryptlex servers when activating. You can see the extra data by clicking any product key link on the product version page.

[![](https://cryptlex.com/public/img/docs/sample-activation-data.png "activation-data")](https://cryptlex.com/public/img/docs/sample-activation-data.png)

### How to pass extra activation data during activation

Passing extra activation data to Cryptlex servers is pretty simple. Just invoke the following function:

```
SetExtraActivationData("Sample activation data");
```

before invoking the activation function:

```
ActivateProduct();
```

This will set the extra data which is then passed to Cryptlex servers during activation. The maximun size of activation data should be less than 256 UTF-8 characters.

### Possible uses of extra activation data

You can use extra activation data to pass on:

* Installed version of your product
* Customer name activating the product
* OS details etc.



