# User object

|Property|Value|Description|
|--|--|
|`id`|int|User id|
|`first_name`|string|User first name|
|`last_name`|string|User last name|
|`is_closed`|bool|Is user profile closed|
|`can_access_closed`|bool|Can you see closed profile|
|`verified`|bool|Is user verified|
|`sex`|int|Gender|
|`has_photo`|bool|Does user has photo|
|`photo_max_orig`, `photo_max`, `photo_50`, `photo_100`, `photo_200`|string|Photo urls|
|`status`|string|Status. If user have audiostatus, returns `status_audio`|
|`screen_name`|string|Users shortcode|
|`friend_status`|int|-|
|`last_seen`|int|User last online|
|`music`|string|Users favourite music|
|`movies`|string|Users favourite films|
|`tv`|string|Users favourite tv shows|
|`books`|string|Users favourite books|
|`city`|string|Users city|
|`interests`|string|Users interests|
|`quotes`|string|Users favourite quotes|
|`email`|string|Users contact email|
|`telegram`|string|Users telegram|
|`about`|string|Users description|
|`rating`|string|Users rating|
|`correct_counters`|array|Array with user's counters|
|`background`|array|Background photo urls|
|`reg_date`|int|User registration date|
|`is_dead`|bool|Is user dead|
|`nickname`|string|Nickname, or "middle name"|
|`blacklisted_by_me`|bool|Is blacklisted by current user|
|`blacklisted`|bool|Is this user blacklisted me|
