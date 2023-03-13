# sudo

`sudo` is a command on most Linux systems that allows you to run a command as another user. It originally stood for "superuser do" but the official expansion is "substitute user, do" however by default sudo runs the command as root.

Of course the system doesn't let just _any_ user run a command as root, so to do this your user needs to reside in the `/etc/sudoers` file.

Some commands need to be ran as root such as changing the ownership of a file

```bash
$ touch file.txt
$ chown root:root file.txt
chown: changing ownership of 'file.txt': Operation not permitted
$ sudo chown root:root file.txt
$
```