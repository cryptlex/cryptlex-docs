# Creating Users

You will usually create users with **admin roles** through the dashboard but creating users with **user or organization-admin** roles for your licenses will be most of the time done using the Web API, when your customer makes a purchase.

Following is a sample request which creates a user with a `user` role:

{% swagger baseUrl="https://api.cryptlex.com" path="/v3/users" method="post" summary="Creating user" %}
{% swagger-description %}
Creates a new user.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Bearer access token.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="firstName" type="string" required="true" %}
First name of the user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="lastName" type="string" required="true" %}
Last name of the user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" required="true" %}
Email address of the user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" type="string" required="true" %}
Password of the user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="role" type="string" required="true" %}
Role of the user - 'user' or 'organization-admin'
{% endswagger-parameter %}

{% swagger-response status="201" description="" %}
```
{
  "name": "John Doe",
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "role": "user",
  "id": "99e2ba70-09ce-4c18-8d6c-2adccb6379b9",
  "createdAt": "2018-05-01T07:53:56.0095476Z",
  "updatedAt": "2018-05-01T07:53:56.0095495Z"
}
```
{% endswagger-response %}
{% endswagger %}

##
