### `docs.add` 🔰

Adds document to user collection

**Params**:

|Name|Value|Description|
|--|--|--|
|`owner_id`|unsigned int|ID of owner|
|`doc_id`|unsigned int|ID of document|
|`access_key`|string|Access key|

**Result**

Returns id of new document

**Possible errors**:

|Code|Description|
|--|--|
|1150|Invalid document id|
|100|One of the parameters specified was missing or invalid: this document already added|
