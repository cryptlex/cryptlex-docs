# Unverified Trials

Unverified trial does not require online activation. All the information regarding trial is only stored on the user's machine in an encrypted form. The trial resets if user formats the PC or deletes the local hidden trial data. This type of trial is not recommended.

As the unverified trial data is completely stored on the user's machine, you can have unlimited trial users and trial can start without an internet connection.

## Adding unverified trial to your app

When your user installs your application first time, invoke `ActivateLocalTrial()` LexActivator API functions to start the trial. Following sample code should be executed once after user installs your app, ideally on a button click. Executing multiple times would will not reset the trial.

```c
int status;
status = ActivateLocalTrial();
if (LA_OK == status)
{
	printf("Product trial activated successfully!");
}
else if (LA_LOCAL_TRIAL_EXPIRED == status)
{
	printf("Product trial has expired!");
}
else
{
	printf("Product trial activation failed: %d", status);
}
```

Once the trial is started you only need to invoke `IsLocalTrialGenuine()` and `GetLocalTrialExpiryDate()` LexActivator API functions at the start of your app after `IsLicenseGenuine()` check. Following is the sample code:

```c
int trialStatus;
trialStatus = IsLocalTrialGenuine();
if (LA_OK == trialStatus)
{
	unsigned int trialExpiryDate = 0;
	GetLocalTrialExpiryDate(&trialExpiryDate);
	int daysLeft = (trialExpiryDate - time(NULL)) / 86500;
	printf("Trial days left: %d", daysLeft);
}
else if (LA_LOCAL_TRIAL_EXPIRED == trialStatus)
{
	printf("Trial has expired!");
}
else
{
	printf("Either trial has not started or has been tampered!");
	// Activate the trial
}
```



