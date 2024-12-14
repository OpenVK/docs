### `wall.post` 🔰

Creates post on wall.

**Params**:

|Name|Value|Description|
|--|--|--|
|`owner_id`|int|Wall id|
|`message`|string|Content|
|`from_group`|bool|Is from group or no|
|`signed`|bool|Is signed or no|
|`attachments`|csv array|Attachments, like photo12827_117,video14812_1,audio1_45|
|`post_id`|unsigned int|Postes post from suggested|
|`lat`|float|Latitude of geopoint|
|`long`|float|Longitude of geopoint|
|`place_name`|string|Custom name of geopoint|

**Results**:

Returns `post_id` field.
