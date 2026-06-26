### `audio.getAlbums` 🔰

Fields: **`owner_id`**, **`playlist_id`**

Returns playlist.

**Result**:

|Name|Value|Description|
|--|--|--|
|`id`|int|Absolute playlist ID|
|`owner_id`|int|Owner's ID|
|`raw_id`|string|Prettyfied ID|
|`title`|string|Playlist's name|
|`cover_url`|string|URL to covers|
|`last_updated`|string|Date when playlist was updated|
|`explicit`, `followed`, `official`, `listens`|int|Dummies, always 0|
|`size`|int|Count of tracks in playlist|
|`covers` and `list`|array|Dummy, currently empty|
|`description` and `raw_description`|array|Playlist description|
