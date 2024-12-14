### `photos.getWallUploadServer` 🔰

Fields: **`group_id`**

Returns the server address for sending group photos for post in a POST request.

!!! caution
    After receiving the address of the attachment sending server, you must specify the `Content-Type` header with the value `multi-part/form-data` in the POST request itself, as well as the file in the `photo` data part.
