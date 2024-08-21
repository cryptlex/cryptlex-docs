# Offline Floating License

## Overview

Offline floating licenses offer flexibility for users to continue accessing licensed functionality even when they are not connected to the LexFloatServer. This feature allows LexFloatServer to lease licenses that can be used outside the company network for a specified duration.

LexFloatServer administrators can set the maximum lease duration using the `maxOfflineLeaseDuration` parameter and control the number of clients that can hold an offline license lease simultaneously with the `allowedOfflineFloatingClients` parameter in the `config.yml`.

### **Requesting an offline floating license**

The `RequestOfflineFloatingLicense()` function in the LexFloatClient allows users to lease an offline license from the LexFloatServer. Once the floating client is leased, it remains valid even when the user is disconnected from the company network. The floating client will automatically expire once the lease duration has elapsed.

The recommended flow for implementing the `RequestOfflineFloatingLicense()` function is as follows:

```jsx
// Always check for existing floating license before leasing the floating license
    status = HasFloatingLicense();
    if (status == LF_OK) {
        printf("Floating license is available.\\n");
    } else {
        printf("Floating license not found: %d\\n", status);
        printf("Please enter the desired lease duration in seconds: ");
        scanf("%u", &leaseDuration); // User input for lease duration

        // Requesting an offline floating license with user-specified duration
        status = RequestOfflineFloatingLicense(leaseDuration);
        if (status != LF_OK) {
            printf("Error code: %d\\n", status);
            return status;
        } else {
            printf("Success! License acquired for %u seconds.\\n", leaseDuration);
        }
    }
```
