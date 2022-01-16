---
layout: post
title:  "Bash script for getting a Google Oauth2 access token"
date:   2018-06-22 16:08:00 +0700
tags:   oauth2 google cli
---
A project from https://console.developers.google.com/ has:
  + client-id
  + secret

Scopes: e.g. [google drive api scopes](https://developers.google.com/drive/api/v3/about-auth#what_scope_or_scopes_does_my_app_need)

We need to get refresh token & access token:
```sh
# Authorization link.  Place this in a browser and copy the code that is returned after you accept the scopes.
https://accounts.google.com/o/oauth2/auth?client_id=[Client Id]&redirect_uri=urn:ietf:wg:oauth:2.0:oob&scope=[Scopes]&response_type=code

# Exchange Authorization code for an access token and a refresh token.
curl -X POST \
     -d 'code=[Authentcation code]&client_id=[Client Id]&client_secret=[Secret]&redirect_uri=urn:ietf:wg:oauth:2.0:oob&grant_type=authorization_code' \
     https://accounts.google.com/o/oauth2/token

# Exchange a refresh token for a new access token.
curl -X POST \
     -d 'client_id=[Client Id]&client_secret=[Secret]&refresh_token=[Refresh token]&grant_type=refresh_token' \
     https://accounts.google.com/o/oauth2/token
```

clj code:
```clj
(-> "https://www.googleapis.com/oauth2/v4/token"
    (http/post {:form-params {:refresh_token refresh-token
                              :client_id     client-id
                              :client_secret client-secret
                              :grant_type    "refresh_token"}
                :as          :json})
    (get-in [:body :access_token]))
```
