# After installation

**If there is empty screen**

Check openvk.yml -> "credentials" -> "eventDB" and set correct `dbname`, `user` and `password`. Or set `enable` on "false", but notifications will be unavailable.

**How to enable gifts?**

Go to openvk.yml -> "preferences" -> set "commerce" to "true". You can add gifts in admin panel later.

<!--**How to give support rights to user?**

Go to `/admin/chandler/groups` -> create new group "Support"

Then go to edit page, "Group Permissions", set "Model" to "openvk\Web\Models\Entities\TicketReply", "Permission" -> "write"

Then go to "Group Members" -> set UID from needed user (you can get it from "/admin/users") -> "Add"-->
