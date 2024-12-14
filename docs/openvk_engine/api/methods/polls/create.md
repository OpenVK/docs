### `polls.create`

Creates new poll, that can be attached after via wall.post, attachments=poll{returned_poll_id}

**Params**:

|Name|Value|Description|
|--|--|--|
|`question`|string|Question of poll|
|`add_answers`|string|Array of answers, like `["yes", "no", "maybe"]`|
|`disable_unvote`|bool|Disable unvote?|
|`is_anonymous`|bool|Is aninymous?|
|`is_multiple`|bool|Is multiple?|
|`end_date`|int|End date.|

**Results**:
Returns new poll object.
