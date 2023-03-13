# Unix User

The Linux kernel supports the traditional concept of a Unix user. A user is an entity that can run processes and own files.

A system can have multiple users, and different permissions can be made so only certain users can access them. A lot of files in `/` only the user **root** can access

Every user-space process has an _owner_ and these processes are said to be run _as_ the owner. The said owner can terminate its own processes, but not interefere with other users processes.

A special user is in most Linux systems called **root** which can terminate and alter any user process and read any file on the system. The term _superuser_ is thus given to root.

You can list all users on a system by `cat`ing `/etc/passwd`

```bash
$ cat /etc/passwd | head -5
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```



