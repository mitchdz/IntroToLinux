# System Monitoring

System Monitoring can be an important part of operating a Linux system.

## Displaying Linux Processes

top - display Linux processes
```bash
$ top
```
ps - report a snapshot of the current processes. This is very powerful
```bash
# a - show process of all users
# u - display the process's user/owner
# x - also show processes not attached to a terminal
$ ps aux
# m - show threads
$ ps m
```

list open files and processes that use them
```bash
$ sudo lsof
```

Tracing program execution and system calls

```bash
$ strace cat /dev/null
```