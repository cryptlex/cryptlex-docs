# User Management

## Roles

Roles helps you manage authorisation, which enables you to specify the resources that users in your application are allowed to access. 

Each account comes with two reserved roles **admin** and **user**.

### Admin Role

Admin role gives your users **\(employees\)** complete control in the account including account deletion. 

{% hint style="info" %}
Any user with **admin** **role** is counted against the admins in your plan.
{% endhint %}

### User Role

User role is meant for your **customers** whom you want to license your product. 

{% hint style="info" %}
Any user with **user** **role**  is counted against the users in your plan.
{% endhint %}

### Custom Roles

Additionally, you can create custom roles with limited permissions and assign them to your users **\(employees\)**.

{% hint style="info" %}
Any user with any **custom** **role** is counted against the admins in your plan.
{% endhint %}

## Creating Users

You will usually create users with **admin role** through dashboard but creating users with **user role** for your licenses will be most of the times done using the web API, when your customer makes a purchase.

Following is a sample request which creates a user with user role:

{% api-method method="post" host="https://api.cryptlex.com" path="/v3/users" %}
{% api-method-summary %}
Creating User
{% endapi-method-summary %}

{% api-method-description %}
Creates a new user.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer access token.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="firstName" type="string" required=true %}
First name of the user.
{% endapi-method-parameter %}

{% api-method-parameter name="lastName" type="string" required=true %}
Last name of the user.
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
Email address of the user.
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=true %}
Password of the user.
{% endapi-method-parameter %}

{% api-method-parameter name="roles" type="array" required=true %}
List of roles, set it to \["user"\]
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
  "name": "John Doe",
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "roles": [
    "user"
  ],
  "id": "99e2ba70-09ce-4c18-8d6c-2adccb6379b9",
  "createdAt": "2018-05-01T07:53:56.0095476Z",
  "updatedAt": "2018-05-01T07:53:56.0095495Z"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Authenticating Users

You can authenticate your users to get the access token of the user which can further be used to get the user profile and list of user licenses.

{% api-method method="post" host="https://api.cryptlex.com" path="/v3/account/login" %}
{% api-method-summary %}
Authenticate user
{% endapi-method-summary %}

{% api-method-description %}
Authenticates the user using the login credentials and returns an access token.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="companyId" type="string" required=true %}
Unique company identifier.
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
Email address of the user.
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=true %}
Password of the user
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR..."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



