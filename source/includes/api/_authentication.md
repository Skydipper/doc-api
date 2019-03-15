# Authentication

The Skydipper API uses JWT [(JSON Web Tokens)](https://tools.ietf.org/html/rfc7519) to identify and authenticate its users. This token must be provided inside an `Authorization` header, with the form `Bearer: <token>`.

However, in order to perform GET requests for content that is not private, there's no need for any sort of authentication or token.

## How to create a new user

To create a new user make a request like the one in the sidebar:

```shell
curl -X POST https://api.skydipper.com/auth/user \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
 '{
    "email":"<email>",
    "role":"<role>",
    "extraUserData": {
      "apps": [
        "<apps>"
      ]
    }
}'
```

There are three allowed roles: `USER`, `MANAGER` and `ADMIN`. The 'apps' field only permits applications that are powered by the API: for now the only application is `skydipper`, but some more will be available in the future.

## How to generate your private token
Endpoint for email + password based login.

```bash
# Email + password based login - JSON format
curl -X POST http://api.skydipper.com/auth/login \
-H "Content-Type: application/json"  -d \
 '{
    "email":"your-email@provider.com",
    "password":"potato"
}'
```

Refer to [user management](#user-management) for more information on the operations available in the Skydipper API for managing user accounts, token generation, etc.
