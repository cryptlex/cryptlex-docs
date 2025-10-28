# Verified Trials

Verified trials are also node-locked. It ensures that trial doesn't reset even if user formats the machine. Each verified trial activation appears in the admin portal in the `Trials -> Trial Activations` section.

{% hint style="info" %}
To ensure proper trial functionality, create a Trial Policy from the `Trials → Trial Policies` page and link it with the corresponding product via  `Home → Products` page.
{% endhint %}

## Adding a verified trial to your app

When your user installs your application for the first time, invoke `ActivateTrial()` LexActivator API functions to start the trial. The following sample code should be executed once after the user installs your app, ideally on a button click. Executing multiple times would unnecessarily re-validate the trial by contacting Cryptlex servers.

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

## Extending trials

You can easily extend the trials so that your customers can get more time to evaluate your product. The trial extension has three steps:

### Getting trial id

You need to get the trial id from your customer. To get the trial id in your app you need to invoke `GetTrialId()` LexActivator API function.

### Extending trial

Go to `Trials -> Trial Activations` section in the admin portal. Paste the "trial id" in the search to find the trial activation.

Then click the "Extend" option in the actions menu. The trial extension form will pop up, add the extension length to extend the trial.

### Re-activate the trial

In your app you need to call `ActivateTrial()` function again, this would extend the trial in user's machine.
