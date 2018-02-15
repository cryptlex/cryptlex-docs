## Trial Extensions

You can easily generate trial extensions for your verfied trials to allow potential customers to fully evaluate your product, ensuring you don't lose a sale

### Generating a Trial Extension

Go to the "Trial Activations" page by clicking "Trial Activations" button below the product version on the products page.

[![](https://cryptlex.com/public/img/docs/products.png "trial-activations")](https://cryptlex.com/public/img/docs/products.png)

On the "Trial Activations" page, click the "Extend Trial" button. You will be presented with a form.

[![](https://cryptlex.com/public/img/docs/trial-extension.png "trial-extensions")](https://cryptlex.com/public/img/docs/trial-extension.png)

Fill in the trial extension length and click "Generate Extension Key" button. You will be prompted to download the extension key.

### Using Trial Extension Key in your App

Now, to extend the trial, you need to use the above generated trial extension key in the`ExtendTrial()`LexActivator API function. Following is the sample code:

```c
    int status;
    status = ExtendTrial("YOUR TRIAL EXTENSION KEY");
    if(status == LA_OK)
    {
        status =  GetTrialDaysLeft(&days, LA_V_TRIAL);
        if(status == LA_OK){
            printf("Days Left: %d",days);
        }
        else{
            printf("Error code: %d",status);
        }
    }
    else{
        printf("Error code: %d",status);
    }
```

**Note:**Trial extensions are only supported for verified trials.

