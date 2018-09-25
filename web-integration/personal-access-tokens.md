# Personal Access Tokens

Personal access tokens can be used by third party applications and scripts to authenticate with the [Cryptlex API](https://api.cryptlex.com/v3/docs). They function similar to API keys and offer fine grained access control.

Once you have your token, you can authenticate your API requests by passing it in the "**Authorization**" header.

```http
Authorization: Bearer {ACCESS_TOKEN}
```

Keep your access tokens secure and do not share them in publicly accessible areas such as Github, client-side code, and so forth.

## Creating a personal access token 

You can easily create personal access tokens through dashboard. Go to the "[Personal Access Tokens](https://app.cryptlex.com/api/personal-access-tokens)" section in the dashboard and click the add the button. A form with following fields will popup:

#### **Name** {#name}

Name for the access token.

#### **Expiration Date** {#url}

Expiration date for the token. Leave empty for no expiry.

#### **Scopes** {#token}

The permissions to restrict the actions the token can be used to perform.

## Revoking a personal access token 

At any time, you can revoke any personal access token by just clicking the  "**Revoke"** option in the "Personal Access Tokens" section.

## Limiting scopes of a personal access token 

Personal access tokens can be created with one or more scopes that allow various actions that a given token can perform. You should always scope the token access to minimum required resources, by adding minimum number of permissions. The available scopes \(permissions\) are depicted in the following table.

| **Scope** | **Description** |
| :--- | :--- |
| `account:read` | Read-only access to the account details. |
| `account:write` | Update and delete account. |
| `activation:read` | Read-only access to all the license activations. |
| `analytics:read` | Read-only access to analytics. |
| `eventLog:read` | Read-only access to event logs. |
| `invoice:read` | Read-only access to all the invoices. |
| `license:read` | Read-only access to all the licenses. |
| `license:write` | Create, update and delete licenses. |
| `licensePolicy:read` | Read-only access to all the license policies. |
| `licensePolicy:write` | Create, update and delete license policies. |
| `paymentMethod:read` | Read-only access to all the credit cards. |
| `paymentMethod:write` | Create, update and delete credit cards. |
| `personalAccessToken:write` | Create, revoke and delete personal access tokens. |
| `product:read` | Read-only access to all the products and related policies. |
| `product:write` | Create, update and delete products. |
| `release:read` | Read-only access to all the releases. |
| `release:write` | Create, update, publish and delete releases. |
| `role:read` | Read-only access to all the roles. |
| `role:write` | Create, update and delete roles. |
| `tag:read` | Read-only access to all the tags. |
| `tag:write` | Create, update and delete tags. |
| `trialActivation:read` | Read-only access to all the trial activations. |
| `trialActivation:write` | Extend and delete trial activations. |
| `trialPolicy:read` | Read-only access to all the trial policies. |
| `trialPolicy:write` | Create, update and delete trial policies. |
| `user:read` | Read-only access to all the users. |
| `user:write` | Create, update and delete users. Generate password reset tokens for users with `USER` role. |
| `webhook:read` | Read-only access to all the webhooks. |
| `webhook:write` | Create, update and delete webhooks. |



