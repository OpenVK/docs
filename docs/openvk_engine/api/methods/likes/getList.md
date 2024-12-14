### `likes.getList` 🔰

Return likes list of item.

**Params**:

|Name|Value|Description|
|--|--|--|
|`type`|string|"post", "comment", "video", "photo", "note"|
|`owner_id`|int|Item owner id|
|`item_id`|int|Item id|
|`extended`|bool|If 0, returns only ids|
|`offset`|unsigned int|Offset|
|`count`|unsigned int|Count|
|`skip_own`|bool|Skip own like or not|

**Result**:

Return `count` and `items` fields.
