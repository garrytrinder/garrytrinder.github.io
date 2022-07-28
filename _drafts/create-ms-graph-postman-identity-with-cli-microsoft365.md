# Using CLI for Microsoft 365 to generate Azure AD app to use with Microsoft Graph Postman Collection

Microsoft Graph is the API to access your data in 

The Postman API client is the foundational tool of Postman, and it enables you to easily explore, debug, and test your APIs while also enabling you to define complex API requests for HTTP, REST, SOAP, GraphQL, and WebSockets. Source: https://www.postman.com/product/tools/


Why would I use this instead of Graph Explorer?

```sh
m365 aad app add \
    --name "Postman" \
    --platform "web" \
    --redirectUris "https://oauth.pstmn.io/v1/callback,https://app.getpostman.com/oauth2/callback" \
    --apisDelegated "https://graph.microsoft.com/Mail.Read" \
    --apisApplication "https://graph.microsoft.com/User.Read.All" \
    --withSecret
```

```json
{
  "appId": "7b2d2dbe-4ebe-4942-aa63-2048ea2e68b2",
  "objectId": "876d8a5a-800f-44a1-b4a4-6baa64281129",
  "tenantId": "e8954f17-a373-4b61-b54d-45c038fe3188",
  "secret": "t5r7Q~ebk2sc_skaru5cwhWKXip_d-iWeFoE5"
}
```