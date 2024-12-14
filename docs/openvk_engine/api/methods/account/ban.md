### `account.ban` 🔰

Adds user to blacklist. 

**Params**:

|Name|Value|Description|
|--|--|--|
|`owner_id`|unsigned int|ID of user|

**Result**

Returns `1` on success.

**Possible errors**:

|Code|Description|
|--|--|
|15|Access denied: cannot blacklist yourself|
|-7856|Blacklist limit exceeded|
