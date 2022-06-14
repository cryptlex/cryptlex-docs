# Creating Users

You will usually create users with **admin role** through dashboard but creating users with **user role** for your licenses will be most of the times done using the web API, when your customer makes a purchase.

Following is a sample request which creates a user with user role:

{% swagger baseUrl="https://api.cryptlex.com" path="/v3/users" method="post" summary="Creating user" %}
{% swagger-description %}
Creates a new user.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer access token.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="firstName" type="string" %}
First name of the user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="lastName" type="string" %}
Last name of the user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
Email address of the user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" type="string" %}
Password of the user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="roles" type="array" %}
List of roles, set it to ["user"]
{% endswagger-parameter %}

{% swagger-response status="201" description="" %}
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
{% endswagger-response %}
{% endswagger %}

##
