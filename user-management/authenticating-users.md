# Authenticating Users

You can authenticate your users to get the access token of the user which can further be used to get the user profile and list of user licenses.

{% swagger baseUrl="https://api.cryptlex.com" path="/v3/accounts/login" method="post" summary="Authenticate user" %}
{% swagger-description %}
Authenticates the user using the login credentials and returns an access token.
{% endswagger-description %}

{% swagger-parameter in="body" name="companyId" type="string" %}
Unique company identifier.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
Email address of the user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" type="string" %}
Password of the user.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR..."
}
```
{% endswagger-response %}
{% endswagger %}

