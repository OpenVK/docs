### `messages.send` 🔰

Fields: **`user_id`**, **`peer_id`**, `domain`, `user_ids`, `message`

Sends a message to user. Will return the message's ID, if successed.

Please be aware that this method will trigger `setOnline` method. To avoid this, simply add `forGodSakePleaseDoNotReportAboutMyOnlineActivity` as field.
