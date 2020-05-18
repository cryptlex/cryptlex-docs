# Authenticating Users

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
Password of the user.
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



