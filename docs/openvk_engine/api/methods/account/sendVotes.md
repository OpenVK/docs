### `account.sendVotes` 🔰

**Warning**: this method is incompatible with VK API.

Send votes to user.

**Params**:
|Name|Value|Description|
|--|--|--|
|`reciever`|unsigned int|ID of reciever|
|`value`|unsigned int|Count of voices|
|`message`|string|Message, that will be seen in notification.|

**Possible errors**:

|Code|Description|
|--|--|
|-105|Commerce is disabled on this instance|
|-248|Invalid reciever id|
|-249|Message is too long|
|-252|Not enough votes|
|-250|Invalid reciever|
|-251|Can't transfer votes to yourself|
