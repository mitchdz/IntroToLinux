# Symlinks

Symlinks are short for **symbolic links**  And a basic symlink looks like

```bash
$ ln -s target linkname
```
(I remember the order as list what you have first, and what you want second)

For example, let's put our test.sh script on `$PATH`
```bash
$ sudo ln -s $(pwd)/test.sh /usr/bin/
$ ls -l /usr/bin/test.sh
lrwxrwxrwx 1 root root 19 Mar 13 21:06 /usr/bin/test.sh -> /home/mitch/test.sh
$ which test.sh
/usr/bin/test.sh
$ test.sh
hello world!
```

You can see above that I called `test.sh` without the leading `./` and that's because the script symbolic link now resides in `/usr/bin/` which is part of $PATH. Now if we change the "original" file, it will also be changed when we call the symlink.

```bash
$ echo "echo 'yay'" >> test.sh
$ test.sh
hello world!
yay
```