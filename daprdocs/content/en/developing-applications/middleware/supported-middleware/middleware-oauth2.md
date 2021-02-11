---
type: docs
title: "OAuth2"
linkTitle: "OAuth2"
weight: 2000
description: "Use Dapr OAuth2 middleware to secure HTTP endpoints"
type: docs
---

The Dapr OAuth2 [HTTP middleware]({{< ref middleware-concept.md >}}) enables the [OAuth2 Authorization Code flow](https://tools.ietf.org/html/rfc6749#section-1.3.1) on a Web API without modifying the application. This design separates authentication/authorization concerns from the application, so that application operators can adopt and configure authentication/authorization providers without impacting the application code.

## Middleware component definition

```yaml
apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
  name: oauth2
spec:
  type: middleware.http.oauth2
  version: v1
  metadata:
  - name: clientId
    value: "<your client ID>"
  - name: clientSecret
    value: "<your client secret>"
  - name: scopes
    value: "https://www.googleapis.com/auth/userinfo.email"
  - name: authURL
    value: "https://accounts.google.com/o/oauth2/v2/auth"
  - name: tokenURL
    value: "https://accounts.google.com/o/oauth2/token"
  - name: redirectURL
    value: "http://dummy.com"
  - name: authHeaderName
    value: "authorization"
```

| Metadata field | Description                                                                                                                                                                  | Example                                        |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| clientId       | The client ID of your application that is created as part of a credential hosted by a OAuth-enabled platform                                                                 |                                                |
| clientSecret   | The client secret of your application that is created as part of a credential hosted by a OAuth-enabled platform                                                             |                                                |
| scopes         | A list of space-delimited, case-sensitive strings of [scopes](https://tools.ietf.org/html/rfc6749#section-3.3) which are typically used for authorization in the application | `"https://www.googleapis.com/auth/userinfo.email"` |
| authURL        | The endpoint of the OAuth2 authorization server                                                                                                                              | `"https://accounts.google.com/o/oauth2/v2/auth"`   |
| tokenURL       | The endpoint is used by the client to obtain an access token by presenting its authorization grant or refresh token                                                          | `"https://accounts.google.com/o/oauth2/token"`     |
| redirectURL    | The URL of your web application that the authorization server should redirect to once the user has authenticated                                                             | `"https://myapp.com"`                              |
| authHeaderName | The authorization header name to forward to your application                                                                                                                 | `"authorization"`                                |
| forceHTTPS     | If true, enforces the use of TLS/SSL                                                                                                                                         | `true`                                         |

## Related links
- [Configure API authorization with OAuth]({{< ref oauth >}})
- [Middleware Quickstart](https://github.com/dapr/quickstarts/tree/master/middleware)
- [Middleware concept]({{< ref middleware-concept.md >}})
- [Dapr configuration]({{< ref configuration-concept.md >}})