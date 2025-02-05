# After installation

**"Table "aliases" does not exist."**

You forgot to apply migration files from %openvk%/install/sqls. <!--To not import all files separately, you may merge them into one file. On Windows: copy *.sql all.sql On UNIX: cat *.sql > .all.sql-->

**Page infinitely reloads**

Set "security" -> "secret" on %chandler%/chandler.yml.

**Empty page with Tracy bar**

Check openvk.yml -> "credentials" -> "eventDB" and set correct `dbname`, `user` and `password`. Also, you can set `enable` to "false", but notifications will be unavailable.

**Nette says that table does not exist, but it's not so**

Try to clean up Nette cache on %chandler%/tmp/cache/database

**How to enable gifts?**

Go to openvk.yml -> "preferences" -> set "commerce" to "true". You can add gifts in the admin panel later.

**How to give support rights to user?** <!--This functionality is broken, but let's pretend it works-->

Go to `/admin/chandler/groups` -> create new group "Support"

Then go to edit page, "Group Permissions", set "Model" to "openvk\Web\Models\Entities\TicketReply", "Permission" -> "write"

Then go to "Group Members" -> set UID from needed user (you can get it from "/admin/users") -> "Add"
