# Creating Users

You will usually create users with **admin roles** through the admin portal but creating users with **user or organization-admin** roles for your licenses will be most of the time done using the Web API, when your customer makes a purchase.

Following is a sample request which creates a user with a `user` role:

## Creating user

<mark style="color:green;">`POST`</mark> `https://api.cryptlex.com/v3/users`

Creates a new user.

#### Headers

| Name                                            | Type   | Description          |
| ----------------------------------------------- | ------ | -------------------- |
| Authorization<mark style="color:red;">\*</mark> | string | Bearer access token. |

#### Request Body

| Name                                        | Type   | Description                                       |
| ------------------------------------------- | ------ | ------------------------------------------------- |
| firstName<mark style="color:red;">\*</mark> | string | First name of the user.                           |
| lastName<mark style="color:red;">\*</mark>  | string | Last name of the user.                            |
| email<mark style="color:red;">\*</mark>     | string | Email address of the user.                        |
| password<mark style="color:red;">\*</mark>  | string | Password of the user.                             |
| role<mark style="color:red;">\*</mark>      | string | Role of the user - 'user' or 'organization-admin' |

{% tabs %}
{% tab title="201 " %}
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
{% endtab %}
{% endtabs %}

##
