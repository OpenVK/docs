# OpenVK API description

OpenVK API is based on VKontakte's API for compatibility. If you want to improve the API, then read [this page](https://github.com/openvk/openvk/blob/master/VKAPI/README.md).

To call the function, you need to go to `/method/` URL, and then, the function name, for example: `/method/Account.getProfileInfo`. The server will return JSON data. You can use GET or POST to send the Data.

🔰 above the function name means it requires authorization.

## Authorization

To get token, you should call the "token" page:

`/token?username={YOUR USERNAME}&password={YOUR PASSWORD}&grant_type=password`

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

## Account

### `getProfileInfo` 🔰

Returns the info about account.

```json
{
    "response":
    {
        "first_name": "Vladimir",
        "id": 1,
        "last_name": "Barinov",
        "home_town": "Moscow",
        "status": "Status example",
        "bdate": "1.1.1970",
        "bdate_visibility": 0,
        "phone": "+420 ** *** 228",
        "relation": 2,
        "sex": 2
    }
}
```

*Some fields are faked for VK API Compatibility*

### `getInfo` 🔰

*This is a dummy function*

```json
{
    "response": {
        "2fa_required": 0,
        "country": "CZ",
        "eu_user": false,
        "https_required": 1,
        "intro": 0,
        "community_comments": false,
        "is_live_streaming_enabled": false,
        "is_new_live_streaming_enabled": false,
        "lang": 1,
        "no_wall_replies": 0,
        "own_posts_default": 0
    }
}
```

### `setOnline` 🔰

Set the online status to current. Always returns `1`.

### `setOffline` 🔰

Dummy function, always returns `1`.

### `getAppPermissions`

Dummy function, always returns `9355263`.

### `getCounters` 🔰

Returns the counters of Unread `Messages`, `Notifications` and `Friends` Requests.

## Friends

### `get`

Fields: **`user_id`**, `fields`, `offset`, `count`

Returns the user's friend ID list with count.

### `getLists` 🔰

Dummy function, always returns 0 items.

### `edit`, `deleteList`, `editList` 🔰

Dummy functions, always return `1`.

### `add` 🔰

Fields: **`user_id`**

Sends a requests to another user or adds user to friends list.

Returns: `1` (friend request sent) or `2` (request from user approved)

### `delete` 🔰

Fields: **`user_id`**

Removes the user from friend list or the request.

Returns `1` if successed, otherwise will throw an error.

### `areFriends` 🔰

Fields: **`user_ids`**

Checks the friendship status with other specified users.

```json
{
    "response": [
        {
            "friend_status": 2,
            "user_id": 2
        },
        {
            "friend_status": 3,
            "user_id": 1
        },
        {
            "friend_status": 1,
            "user_id": 6
        }
    ]
}
```

## Groups

### `get` 🔰

Fields: `user_id`, `fields`, `offset`, `count` _6_

Returns the user's groups list with count.

`fields`: `verified`, `has_photo`, `photo_max_orig`, `photo_max`, `photo_50`, `photo_100`, `photo_200`, `photo_200_orig`, `photo_400_orig`, `members_count`

### `getById`

Fields: **`groups_id`** or **`group_id`**, `fields`

Returns the info about group(s).

`fields`: `verified`, `has_photo`, `photo_max_orig`, `photo_max`, `photo_50`, `photo_100`, `photo_200`, `photo_200_orig`, `photo_400_orig`, `members_count`, `site`, `description`, `contacts`, `can_post`, `is_member`

### `search`

Fields: **`q`**, `offset`, `count`

Searches for groups.

## Likes

### `add` 🔰

Fields: `type`, `owner_id`, `item_id`

Likes the object. Returns count of likes.

`type`: `post`

### `delete` 🔰

Fields: `type`, `owner_id`, `item_id`

Removes like from the object. Returns count of likes.

`type`: `post`

### `isLiked` 🔰

Fields: `user_id`, `type`, `owner_id`, `item_id`

Checks if user liked the object or not.

`type`: `post`

## Messages

### `getById` 🔰

Fields: **`message_ids`**, `preview_length`, `extended`

Returns the messages by it's IDs.

### `send` 🔰

Fields: **`user_id`**, **`peer_id`**, `domain`, `user_ids`, `message`

Sends a message to user. Will return the message's ID, if successed.

### `delete` 🔰

Fields: **`message_ids`**

Deletes the message.

### `restore` 🔰

Fields: **`message_ids`**

Restores deleted message.

### `getConversations` 🔰

Fields: `offset`, `count` _20_, `filter`, `extended`

Returns user's chat list.

### `getConversationsById` 🔰

Fields: **`peer_ids`**, `extended`, `fields`

Returns the user's chats by their peer IDs.

### `getHistory` 🔰

Fields: `offset`, `count` _20_, `user_id`, `peer_id`, `start_message_id`, `rev`

Returns chat's history.

### `getLongPollHistory` 🔰

Fields: `ts`, `preview_length`, `events_limit`, `msgs_limit`

Return's LongPoll history.

**Check [this](https://vk.com/dev/using_longpoll) if you don't know what is a LongPoll.**

### `getLongPollServer` 🔰

Fields: `need_pts`, `lp_version`, `group_id`

Returns the address to LongPoll server.

**Check [this](https://vk.com/dev/using_longpoll) if you don't know what is a LongPoll.**

## Ovk (aka OpenVK specific methods)

### `version`

Returns the OpenVK version installed on an instance.

### `test`

Returns the information about access token.

### `chickenWings`

Returns `крылышки` string.

### `aboutInstance`

Fields: **`fields`**, `admin_fields`, `group_fields`.

Returns information about the instance, including stats, administrators, most popular groups and links.

`fields`: `statistics`, `administrators`, `popular_groups`, `links`

`admin_fields` are the same as with `Users.get` function.`group_fields` are the same as with `Groups.getById` function.

## Polls

### `getById`

Fields: **`poll_id`**, `extended`, `fields`

Returns poll info. Formatting is the same as it would be in Wall's methods.

### `addVote` 🔰

Fields: **`poll_id`**, **`answers_ids`**

Adds a vote to poll.

### `deleteVote` 🔰

Fields: **`poll_id`**

Removes the vote, except if it is not revotable or it is locked.

## Utils

### `getServerTime`

Returns the time on the server.

## Users

### `get`

Fields: **`user_ids`**, `fields`, `offset`, `count`.

Returns information about user or users.

`fields`: `verified`, `sex` (not the orientation but the gender), `has_photo`, `photo_max_orig`, `photo_max`, `photo_50`, `photo_100`, `photo_200`, `photo_200_orig`, `photo_400_orig`, `status`, `screen_name` (aka short url), `friend_status`, `last_seen`, `music`, `movies`, `tv`, `books`, `city`, `interests`

### `getFollowers` 🔰

Fields: **`user_id`**, `fields`, `offset`, `count` _100_

Returns the followers of user.

### `search`

Fields: **`q`**, `fields`, `offset`, `count` _100_

Searches the users by name, surname or bio, and returns the list.

`Fields` are the same as with `get` function.

## Wall

### `get`

Fields: **`owner_id`**, `offset`, `count` _30_, `extended`

Returns the posts on the wall. `Extended` parameter will also return profile info.

### `getById` 🔰

Fields: **`posts`**, `fields`, `extended`

Returns post(s) by pretty ID (like 1_3 or 32_3).

### `post` 🔰

Fields: **`owner_id`**, **`message`**, `from_group`, `signed`

Creates new post on wall.

Also, there is a way to upload picture or video, just send the media named "photo" or "video" in your post request.

### `repost` 🔰

Fields: **`object`**, `message`

Reposts (copies) a post to a user wall by pretty ID (like wall-1246_747 or wall6_436).

### `createComment` 🔰

Fields: **`owner_id`**, **`post_id`**, **`message`**, `from_group`

Adds a comment to a post on a user wall or community wall.

### `deleteComment` 🔰

Fields: **`comment_id`**

Deletes a comment on a post on a user wall or community wall.

### `getComment` 🔰

Fields: **`owner_id`**, **`comment_id`**, `extended`, `fields`

Returns the info about comment.

### `getComments` 🔰

Fields: **`owner_id`**, **`post_id`**, `need_likes`, `offset`, `count` _10_, `fields`, `sort`, `extended`

Returns a list of comments on a post on a user wall or community wall.

## Newsfeed

### `get` 🔰

Fields: `fields`, `start_from` or `offset`, `count`, `extended`

Returns posts from newsfeed.

### `getGlobal` 🔰

Same as `get`, but this time it outputs global feed.

# Error

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
