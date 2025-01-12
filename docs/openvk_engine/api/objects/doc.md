# Document object

| Property | Value | Description |
|---|---|---|
|`id`|int|Document id|
|`owner_id`|int|Document owner id|
|`title`|string|Document title|
|`size`|int|Document size|
|`ext`|string|Document extension|
|`url`|string|Document URL|
|`date`|timestamp|Document upload time|
|`type`|range(1-8)|Document VK API type|
|`is_hidden`|bool|Is owner hidden|
|`folder_id`|int|0 — private, 3 — public|
|`access_key`|string|Access key|
|`can_manage`|bool|Can current user modify this document|
|`preview`|array|Contains photo object with preview (on images)|
|`tags`|array|Tags array|
