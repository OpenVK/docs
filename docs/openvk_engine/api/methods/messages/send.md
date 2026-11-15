### `messages.send` 🔰

Fields: **`user_id`**, **`peer_id`**, `domain`, `peer_ids`, `user_ids`, `message`, `sticker_id`, `unnoticed`, `attachment`, `reply_to`, `forward`, `forward_messages`

Sends a message to user. Will return the message's ID, if successed.

Please be aware that this method will trigger `setOnline` method. To avoid this, simply add `forGodSakePleaseDoNotReportAboutMyOnlineActivity` as field.
