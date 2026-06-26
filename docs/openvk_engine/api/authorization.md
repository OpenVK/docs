There are two types of authorization. One, that is intended for apps, and second for apps and web applications.

Current OpenVK's official instance is located at https://api.openvk.org/. Don't try to visit this link, it will redirect you back - this domain is made special for API requests because of Anti-DDOS limitations. 

## Password authorization

To get token, you should call the "token" page:

`https://{YOUR DOMAIN}/token?username={YOUR USERNAME}&password={YOUR PASSWORD}&grant_type=password`

Replace `{YOUR DOMAIN}`, `{YOUR USERNAME}` and `{YOUR PASSWORD}` to it's proper value.

You'll get a response like this:

```json
{
    "access_token": "THERE IS A TOKEN. A LONG TOKEN ACTUALLY",
    "expires_in": 0,
    "user_id": 1
}
```

If you need to call the function that requires a token, just put the `access_token` into your GET or POST request, or in HTTP header "Authorization" as Bearer token.

If you have two-factor authorization turned on, either sumbit the code via `request_uri` in Web or pass the 2FA code to the `code` field.

### Client name

At this moment, OpenVK API apps are not implemented. But you can set client name for your token: for this, pass `client_name` param at token endpoint. This name will be seen in some parts of site (online mark and post).

## OAuth

To get token via OAuth, you should call the "authorize" page:

`https://{YOUR DOMAIN}/authorize?client_name={YOUR CLIENT NAME}&redirect_uri={REDIRECT URI}&display=page&response_type=token&revoke={0|1}`

You can set any URL at `redirect_uri`. For apps, we recommend setting this to "https://{YOUR DOMAIN}/blank.html".

For passing access_token as HTTP GET parameters, set `response_type` to `php`.

On `revoke`=1 old token will be revoked.

Additional params: `prefers_postMessage`, `accepts_stale`.

## Token revoking

As api apps are not implemented, you cannot revoke individual token, but you can revoke all tokens at once: for this, go to /settings?act=security -> "End all sessions".
