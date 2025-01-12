### `docs.delete` 🔰

Deletes document from user collection.

**Params**:

|Name|Value|Description|
|--|--|--|
|`owner_id`|unsigned int|ID of owner|
|`doc_id`|unsigned int|ID of document|

**Result**

Returns 1 on success.

**Possible errors**:

|Code|Description|
|--|--|
|1150|Invalid document id|
|1153|Access to document is denied|
