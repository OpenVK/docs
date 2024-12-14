# Audio object

| Property | Value | Description |
|----------|----------|----------|
| unique_id | string   | Encrypted audio id   |
| id    | int   | Audio id   |
| artist    | string   | Peformer   |
| title    | string   | Audios name   |
| duration    | int   | Audio duration in seconds   |
| album_id    | NULL   | Always `NULL`.  |
| url    | string   | A link to the original audio file. Can be disabled on instance and return a link to nomusic.mp3.  |
| manifest    | string   | Link to MPEG-DASH manifest.  |
| keys    | Array   | Keys for manifest.  |
| genre_id    | int   | Genre id of the track.  |
| genre_str    | string   | String with genre name.  |
| lyrics    | int   | You can get actual lyrics by `audio.getLyrics`.  |
| added    | bool   | Does the user's collection contain this audio??  |
| editable    | bool   | Can audio be edited by current user?  |
| searchable    | bool   | Is it possible to find audio in search?  |
| explicit    | bool   | Is this audio obscene?  |
| withdrawn    | bool   | Was it removed for copyright infringement?  |
| ready    | bool   | Was this audio processed?  |
