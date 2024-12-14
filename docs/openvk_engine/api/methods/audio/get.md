### `audio.get` 🔰

Returns audios with some conditions.

**Params**:

|Name|Value|Description|
|--|--|--|
|`owner_id`|int|If passed, returns audios from user/club's collection|
|`album_id`|unsigned int|If passed, returns audios from playlist|
|`audio_ids`|string|If passed, returns audios by ids|
|`offset`|unsigned int|Offset.|
|`count`|unsigned int|Count.|
|`uploaded_only`|bool|If passed, returns only uploaded audios by user|

**Result**:

Returns `count` and `items` fields.
