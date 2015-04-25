# chmod

## Sticky Bit (t permission flag)

* **`chmod 1000`** - set sticky bit (t bit)

* **`chmod +t`** - the same as the previous one
* **`chmod -t`** - unset sticky bit

[Sticky Bit](http://www.linuxnix.com/2012/01/sticky-bit-set-linux.html) is mainly used on folders in order to avoid deletion of a folder and its content by other users though they having write permissions on the folder contents. If Sticky bit is enabled on a folder, the folder contents are deleted by only owner who created them and the root user. No one else can delete other users data in this folder(Where sticky bit is set). This is a security measure to avoid deletion of critical folders and their content(sub-folders and files), though other users have full permissions.

## setuid (s permission flag on user)

Short for "set user ID upon execution".

* **`chmod 4000`** - effective command that runs setuid and sets uid flag

* **`chmod u+s`** - the same as the previous one
* **`chmod u-s`** - unsets uid flag

When an executable file has been given the setuid attribute, normal users on the system who have permission to execute this file gain the privileges of the user who owns the file (commonly root) within the created process. When root privileges have been gained within the process, the application can then perform tasks on the system that regular users normally would be restricted from doing. The invoking user will be prohibited by the system from altering the new process in any way, such as by using ptrace, LD_LIBRARY_PATH or sending signals to it (signals from the terminal will still be accepted, however).

While the setuid feature is very useful in many cases, its improper use can pose a security risk if the setuid attribute is assigned to executable programs that are not carefully designed. Due to potential security issues, many operating systems ignore the setuid attribute when applied to executable shell scripts.

## setgid (s permission flag on directory)

Short for "set group ID on upon execution"

**`chmod 2000`** - set gid flag on directory

**`chmod g+s`** - the same as the previous one
**`chmod g-s`** - unset gid flag on directory

Setting the setgid permission on a directory ("chmod g+s") causes new files and subdirectories created within it to inherit its group ID, rather than the primary group ID of the user who created the file (the owner ID is never affected, only the group ID). Newly created subdirectories inherit the setgid bit. Thus, this enables a shared workspace for a group without the inconvenience of requiring group members to explicitly change their current group before creating new files or directories. Note that setting the setgid permission on a directory only affects the group ID of new files and subdirectories created after the setgid bit is set, and is not applied to existing entities.

## Working mechanics

* `chmod 4700 file` - a user tries to execute the file. First, the user owner is checked. Then the user owner's permissions are checked - in this case 7. Permission is then given. Essentially - the last two numbers have been ignored.
* `chmod 2070 file` - a user tries to execute the file. First, the group owner is checked. Then the file's group permissions are checked - in this case 7. Permission is then given. Essentially - the zeros are ignored.
* `chmod 2070 directory` - a user creates a file inside the directory. The group owner of the directory is checked. Then the file is given the same group permissions as the directory.

## Rule of thumb

The general rule of thumb for setuid and setgid should always be, "Don't Do It." It is only in rare cases that it is a good idea to use either of these file permissions, especially when many programs might have surprising capabilities that, combined with setuid or setgid permissions, could result in shockingly bad security. In those rare cases, though, the setuid and setgid permissions can be used to improve security, when used properly.
