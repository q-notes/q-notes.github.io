---
layout: post
title:  "OAuth2 Grant Types"
date:   2018-07-18 20:10:00 +0700
tags:   oauth2
---

OAuth2 provides several `grant types` for different use cases.

### Authorization Code Grant

![Authorization Code Grant]({{ "/assets/authorization_code_grant.png" | absolute_url }})

### Implicit Grant

Previously, it was recommended that browser-based apps use the "Implicit" flow, which returns an access token immediately in the redirect and does not have a token exchange step. The industry best practice has changed to recommend that the authorization code flow be used without the client secret.

- https://tools.ietf.org/html/rfc8252#section-8.2
- https://oauth.net/2/pkce/

![Implicit Grant]({{ "/assets/implicit_grant.png" | absolute_url }})

### Password Grant

![Password Grant]({{ "/assets/password_grant.png" | absolute_url }})

### Client Credentials Grant
This grant is suitable for machine-to-machine authentication where a specific user’s permission to access data is not required.

![Client Credentials Grant]({{ "/assets/client_credentials_grant.png" | absolute_url }})

### Refresh Token Grant

![Refresh Token Grant]({{ "/assets/refresh_token_grant.png" | absolute_url }})
