### `execute` 🔰

Execute method. Javascript-like scripting language, where you can make up to 25 API calls to generate complex results in one go. Server will compile your code and execute it.

Scripting language support this features:

* Arithmetic operations: `+` `-` `*` `/` `%`
* Variables: `var a`
* Conditions: `if`, `else`
* Loops: `while`, `for`, `break`, `continue`
* Object and array literals: `{key: "value", 'another_key': 123}`, `['a', 123, {}, someVariable]`
* API calls: `API.method({parameters})`
* Object array field selection operator `@.`.
* Functions: `parseInt` and `parseDouble`
* Methods on arrays: `push`, `pop`, `slice`, `splice`, `shift`, `unshift`, `indexOf`
* Methods on strings: `substr`, `split`, `indexOf`
* The `.length` property on strings and arrays
* The special `Args` object that contains any extra parameters you passed to this method
* The `delete` operator to remove fields from objects, e.g. `delete groups[i].description;`
* `//` and `/* ... */` comments

### Code examples

Get posts and notes count for user:

```
var p=API.wall.get({owner_id:1});
var n=API.notes.get({user_id:1});
return [p.count,n.count];
```

Get likes and comments counts from photo:

```
var p=API.photos.getById({"photos":"1_136","extended":1}); 
return {"pid":p@.id,"likes":p@.likes,"comments":p@.comments,"can_comment":p@.can_comment,"tags":p@.tags};
```

Check if user can post on wall:

```
return API.wall.getById({"posts":"1_164"})[0].comments.can_post;
```

### References

* https://web.archive.org/web/20150429005235/http://vk.com/dev/execute
* https://smithereen.software/docs/api/methods/execute