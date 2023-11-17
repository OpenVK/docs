# Playlist object

| Property | Value | Description |
|----------|----------|----------|
| id | int   | Playlist ID |
| owner_id | int   | Playlist creator ID |
| title | string   | Playlist name |
| description | string   | Playlist description |
| size | int   | Number of tracks in the playlist |
| length | int   | Length of all songs in the playlist in seconds |
| created | int   | UNIX-timestamp of playlist creation time |
| modified | int   | UNIX-timestamp of playlist edit time |
| accessible | bool   | Can this user view this playlist? |
| editable | bool   | Can this user edit this playlist? |
| bookmarked | bool   | Is there a playlist in the user's collection? |
| listens | bool   | Number of playlist listens |
| cover_url | bool   | Link to playlist cover |