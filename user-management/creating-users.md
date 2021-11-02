# Creating Users

You will usually create users with **admin role** through dashboard but creating users with **user role** for your licenses will be most of the times done using the web API, when your customer makes a purchase.

Following is a sample request which creates a user with user role:

{% api-method method="post" host="https://api.cryptlex.com" path="/v3/users" %}
{% api-method-summary %}
Creating user
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

## 

