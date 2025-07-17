# Personal Access Tokens

## Access Tokens

Access Tokens in Cryptlex allow you to authenticate API requests without using your account credentials. These tokens are scoped, time-bound, and revocable, offering a secure way to interact with Cryptlex services programmatically.

### Use Cases

* Automating license and release management via the Cryptlex API
* Integrating with CI/CD pipelines
* Connecting third-party tools or internal scripts to Cryptlex

### Steps to Create an Access Token

1. **Navigate to** [`Developer -> Access Tokens`](https://app.cryptlex.com/developer/access-tokens) page from the sidebar in the admin portal.
2. Click the **Create** button.
3. In the popup:
   * **Enter a name** for the token.
   * **Set an expiration date** if needed.
   * **Assign permissions** by selecting the required scopes (Read or Write access) for each module (e.g., Activations, Releases, Licenses, etc.).
4. Click **Create**.
5. On the next screen, **copy the access token** securely. This token will not be visible again.

{% hint style="info" %}
Important: Store the token securely. If exposed or no longer required, you can revoke it from the same Access Tokens page.
{% endhint %}

### Permissions Overview

Each token can be customized with fine-grained permissions:

* **Read**: Allows retrieving data (e.g., list licenses, get release details).
* **Write**: Allows performing actions (e.g., create licenses, update releases).
