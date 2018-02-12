## Verified Trials

Verified trial uses online activation. It ensures that trial doesn't reset even if user formats the machine. Each verified trial activation appears in the dashboard in the trial activations section.

As the count of trial activations is usually much higher than product activations,**TEN**trial activations consume**ONE**activation from your plan. When a trial user activates using a product key, trial activation registered against the user's machine is automatically freed up, hence allowing more trial activations.

### Adding Verified Trial to your App

To add verified trial to your app you need the**Trial Key**. Each product version has one Trial Key which can be used to activate that product version. To get your Trial Key click "Trial Activations" button below the product version on the products page.

[![](https://cryptlex.com/public/img/docs/trial-key.png "trial-key")](https://cryptlex.com/public/img/docs/trial-key.png)

When your user installs your application first time, invoke`SetTrialKey()`and`ActivateTrial()`LexActivator API functions to start the trial. Following sample code should be executed once after user installs your app, ideally on a button click. Executing multiple times would unnecessarily re-validate the trial by contacting Cryptlex servers.

```c
int trialStatus;trialStatus =SetTrialKey("YOUR TRIAL KEY");
if (LA_OK !=status)
{
   printf("Error code: %d",status);
   getchar();
   return status;
}

trialStatus =ActivateTrial();
if (LA_OK ==trialStatus)
{
   unsigned int daysLeft =0;
   GetTrialDaysLeft(&daysLeft,LA_V_TRIAL);
   printf("Trial started, days left: %d",daysLeft);
}
else
{
   //Trial was tampered or has expired
   printf("Trial activation failed: %d",trialStatus);
}
```

Once the trial is started you only need to invoke`IsTrialGenuine()`and`GetTrialDaysLeft()`LexActivator API functions at the start of your app after`IsProductGenuine()`check. Following is the sample code:

```c
int trialStatus;
trialStatus =IsTrialGenuine();
if (LA_OK ==trialStatus)
{
    unsigned int daysLeft =0;
    GetTrialDaysLeft(&daysLeft,LA_V_TRIAL);
    printf("Trial days left: %d",daysLeft);
}
else if (LA_T_EXPIRED == trialStatus)
{
    printf("Trial has expired!");
}
else
{
    printf("Either trial has not started or has been tampered!");
}
```

`IsTrialGenuine()`function verifies the validity of trial. If`IsTrialGenuine()`function detects that trial has been tampered or system time has been changed since activation of trial, it internally sets remaining trial days to zero.

