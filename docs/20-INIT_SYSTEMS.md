# Init Systems

User space starts in roughly this order:
1. init
2. Essential low-level services such as udevd and syslogd
3. Network configuration
4. Mid- and high-level services (cron, printing, and so on)
5. Login prompts, GUIs, and other high-level applications


The init program is a user-space program like any other program on the Linux system, and you’ll find it in `/sbin` along with many of the other system binaries. Its main purpose is to start and stop the essential service processes on the system, but newer versions have more responsibilities.

There are 2 major implementations of init in Linux distributions:
* System V init. A traditional sequenced init (Sys V, usually pronounced “sys-five”). 
* systemd. The emerging standard for init. Many distributions have moved to systemd, and most that have not yet done so are planning to move to it.


System V init is a very traditional init system, but all tasks are sequential which created not the best performance. Newer init systems aimed to solve that by doing multiple tasks in parallel.

You can view all your systemd units with

```bash
systemctl list-units
```

Let's create some systemd units

in `/usr/lib/systemd/system` create the following


create `test1.target` with contents
```bash
[Unit]
Description=test 1
```

create `test2.target` with contents
```bash
[Unit]
Description=test 2
Wants=test1.target
```

And then start `test2.target` with 

```bash
$systemctl start test2.target
```

Now view the status of both units

```bash
$ systemctl status test1.target test2.target
● test1.target - test 1
     Loaded: loaded (/lib/systemd/system/test1.target; static)
     Active: active since Mon 2023-03-13 22:50:34 UTC; 13s ago
      Until: Mon 2023-03-13 22:50:34 UTC; 13s ago

Mar 13 22:50:34 backup systemd[1]: Reached target test 1.

● test2.target - test 2
     Loaded: loaded (/lib/systemd/system/test2.target; static)
     Active: active since Mon 2023-03-13 22:50:34 UTC; 13s ago
      Until: Mon 2023-03-13 22:50:34 UTC; 13s ago

Mar 13 22:50:34 backup systemd[1]: Reached target test 2.
```



---


You can view some systemd unit files in `/usr/lib/systemd/system/`

And you can view the status of any service with

```
$ sudo systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; disabled; preset: enabled)
    Drop-In: /etc/systemd/system/ssh.service.d
             └─00-socket.conf
     Active: active (running) since Sun 2023-02-26 16:36:11 UTC; 2 weeks 1 day ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 96055 (sshd)
      Tasks: 1 (limit: 9396)
     Memory: 7.5M
        CPU: 331ms
     CGroup: /system.slice/ssh.service
             └─96055 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"
```