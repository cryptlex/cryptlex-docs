# Verified Trials

Verified trials are also node-locked. It ensures that trial doesn't reset even if user formats the machine. Each verified trial activation appears in the dashboard in the trial activations section.

## Adding Verified Trial to your App

When your user installs your application first time, invoke `ActivateTrial()` LexActivator API functions to start the trial. Following sample code should be executed once after user installs your app, ideally on a button click. Executing multiple times would unnecessarily re-validate the trial by contacting Cryptlex servers.

```c
int status;
status = SetTrialActivationMetadata("key1", "value1");
if (LA_OK != status)
{
	// handle error
}
status = ActivateTrial();
if (LA_OK == status)
{
	printf("Product trial activated successfully!");
}
else if (LA_TRIAL_EXPIRED == status)
{
	printf("Product trial has expired!");
}
else
{
	printf("Product trial activation failed: %d", status);
}
```

Once the trial is started you only need to invoke `IsTrialGenuine()` and `GetTrialExpiryDate()` LexActivator API functions at the start of your app after `IsLicenseGenuine()` check. Following is the sample code:

```c
int trialStatus;
trialStatus = IsTrialGenuine();
if (LA_OK == trialStatus)
{
	unsigned int trialExpiryDate = 0;
	GetTrialExpiryDate(&trialExpiryDate);
	int daysLeft = (trialExpiryDate - time(NULL)) / 86500;
	printf("Trial days left: %d", daysLeft);
}
else if (LA_TRIAL_EXPIRED == trialStatus)
{
	printf("Trial has expired!");
}
else
{
	printf("Either trial has not started or has been tampered!");
	// Activate the trial
}
```

If `IsTrialGenuine()` does not return a success code you should re-activate the trial.

## Extending Trials

You can easily extend the trials so that your customers can get more time to evaluate your product. Trial extension has three steps:

### Getting Trial Id

You need to get the trial id from your customer. To get the trial id in your app you need to invoke `GetTrialId()` LexActivator API function.

### Extending Trial

Go to "Trial Activations" section in the dashboard. Paste the "trial id" in the search to find the trial activation.

Then go to the "Trial Activation" page and click the "Extend Trial" button. The trial extension form will pop up, add the extension length to extend the trial.

### Re-activate the Trial

In your app you need to call ActivateTrial\(\) function again, this would extend the trial in user machine.

