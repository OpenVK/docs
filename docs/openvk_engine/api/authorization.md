## Password authorization

To get token, you should call the "token" page:

`{YOUR DOMAIN}/token?username={YOUR USERNAME}&password={YOUR PASSWORD}&grant_type=password`

You'll get a response like this:

```json
{
    "access_token": "THERE IS A TOKEN. A LONG TOKEN ACTUALLY",
    "expires_in": 0,
    "user_id": 1
}
```

If you need to call the function that requires a token, just put the `access_token` into your GET or POST request.

If you have two-factor authorization turned on, add a `code` field to your POST request and fill it with, you guessed it, authorization code.

**Client name**

At this moment, OpenVK API apps are not implemented. But you can set client name for your token: for this, pass `client_name` param at token page:

`{YOUR DOMAIN}/token?username={YOUR USERNAME}&password={YOUR PASSWORD}&grant_type=password&client_name={YOUR CLIENT NAME}`

This name will be seen in some parts of site (online mark and post).

## OAuth

To get token via OAuth, you should call the "authorize" page:

`{YOUR DOMAIN}/authorize?client_name={YOUR CLIENT NAME}&redirect_uri=&display=page&response_type=token&revoke={0|1}`

You can set any URL at `redirect_uri`, but we will set "https://oauth.vk.com/blank.html".

On `revoke`=1 old token will be revoked.

Additional params: `prefers_postMessage`, `accepts_stale`.

## Token revoking

As api apps are not implemented, you cannot revoke individual token, but you can revoke all tokens at once: for this, go to {YOUR DOMAIN}/settings?act=security -> "End all sessions".
