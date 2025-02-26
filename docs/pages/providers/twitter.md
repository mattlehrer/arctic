---
title: "Twitter"
---

# Twitter

Add the `offline.access` scope to get refresh tokens.

For usage, see [OAuth 2.0 provider with PKCE](/guides/oauth2-pkce).

```ts
import { Twitter } from "arctic";

const twitter = new Twitter(clientId, clientSecret, redirectURI);
```

```ts
const url: URL = await twitter.createAuthorizationURL(state, codeVerifier, {
	// optional
	scopes
});
const tokens: TwitterTokens = await twitter.validateAuthorizationCode(code, codeVerifier);
const tokens: TwitterTokens = await twitter.refreshAccessToken(refreshToken);
```

## Get user profile

Add the `users.read` scope and use the [`/users/me` endpoint](https://developer.twitter.com/en/docs/twitter-api/users/lookup/api-reference/get-users-me).

```ts
const url = await twitter.createAuthorizationURL(state, codeVerifier, {
	scopes: ["users.read"]
});
```

```ts
const tokens = await twitter.validateAuthorizationCode(code, codeVerifier);
const response = await fetch("https://api.twitter.com/2/users/me", {
	headers: {
		Authorization: `Bearer ${tokens.accessToken}`
	}
});
const user = await response.json();
```
