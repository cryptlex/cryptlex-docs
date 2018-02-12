## Unverified Trials

Unverified trial does not require online activation. All the information regarding trial is only stored on the user's machine in an encrypted form. The trial resets if user formats the PC or deletes the local hidden trial data. This type of trial is not recommended.

As the unverified trial data is completely stored on the user's machine, you can have unlimited trial users and trial can start without an internet connection.

### Adding Unverified Trial to your App

To add unverified trial to your app, you only need to invoke`InitializeTrial()`and`GetTrialDaysLeft()`LexActivator API functions at the start of your app. Following is the sample code:

```
int trialStatus,trialLength; 
trialLength =30; // Must be same as set in the dashboard for the product version
trialStatus =InitializeTrial(trialLength);
if (LA_OK ==trialStatus)
{
   unsigned int daysLeft =0;
   GetTrialDaysLeft(&daysLeft,LA_UV_TRIAL);
   printf("Trial days left: %d",daysLeft);
}
else if (LA_T_EXPIRED ==trialStatus)
{
   printf("Trial has expired!");
}
else
{
   //Trial may have been tampered
   printf("Error code: %d",status);
}
```

`InitializeTrial()`function starts the trial if trial has not started yet and if trial has already started, it verifies the validity of trial. If`InitializeTrial()`function detects that trial has been tampered or system time has been changed since activation of trial, it internally sets remaining trial days to zero.

