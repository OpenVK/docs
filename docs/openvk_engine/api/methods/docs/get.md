### `docs.get` 🔰

Gets documents from current user/club collection.

**Params**:

|Name|Value|Description|
|--|--|--|
|`count`|unsigned int|Count|
|`offset`|unsigned int|Offset|
|`type`|int|VK API type of document|
|`owner_id`|int|Owner ID|
|`return_tags`|bool (0, 1)|Return "tags" field|
|`order`|int (0,1,2)| |

**Result**

Returns `count` and `items` fields.
