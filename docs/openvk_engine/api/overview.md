# OpenVK API description

OpenVK API is based on VKontakte's API for compatibility. If you want to improve the API, then read [this page](https://github.com/openvk/openvk/blob/master/VKAPI/README.md).

To call the function, you need to go to `{YOUR DOMAIN}/method/` URL, and then, the function name, for example: `{YOUR DOMAIN}/method/Account.getProfileInfo`. The server will return JSON data. You can use GET or POST to send the Data.

🔰 above the function name means it requires authorization.

You can read about authorization [there](authorization.md).

## Main params

There are three types of return format.

### Plain JSON

JSON is default. That's it.

### Callback

Sets `Content-Type` header to `application/javascript` and wraps json response into function call. This will allow to bypass CORS limits. Does not work with `auth_mechanism`=`roaming`.

### MessagePack

That's what VK was started using recently. They're hyperfixed with it.

Set `X-Response-Format` to `msgpack` to get response in MessagePack formats.

## Tips

- Main instance API URL is `https://api.openvk.org/method/`

- If there is no description of the method you need, check it on https://dev.vk.ru/ru/method

- To set group, add minus to id

### Adapting your app from VK?

- **Report any inconsistency in the responses to OpenVK developers.** They're trying hard to correct API responses as close as possible.

- Replace `api.vk.ru` and `oauth.vk.ru` to just one domain that user can select or type by themself. We recommend using `api.openvk.org` as default instance.

- In Post object, there's an `explicit` integer parameter. If it's 1, well, it contains NSFW content and it's content should be blurred or hidden behind some kind of button. To prefer user's settings, check [account.getOvkSettings](/docs/openvk_engine/api/methods/account/getOvkSettings) and `nsfw_tolerance` parameter.

- Some instances have multiple domains. To get a list of it and correctly redirect links to app deeplinks, use [ovk.getMirrors](/docs/openvk_engine/api/methods/ovk/getMirrors) method.

## Error

If something goes wrong, the server will return you an error like this:

```json
{
    "error_code": 28,
    "error_msg": "Invalid username or password",
    "request_params":
    [
        {
            "key": "grant_type",
            "value": "password"
        },
        {
            "key": "password",
            "value": "agreatpassword"
        },
        {
            "key": "username",
            "value": "cooluser@cock.li"
        },
        {
            "key": "method",
            "value": "internal.acquireToken"
        },
        {
            "key": "oauth",
            "value": 1
        }
    ]
}
```
