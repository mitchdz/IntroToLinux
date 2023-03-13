# How the Kernel Boots


A simplified view of the boot process looks like this:
1. The machine’s BIOS or boot firmware loads and runs a boot loader.
2. The boot loader finds the kernel image on disk, loads it into memory, and starts it.
3. The kernel initializes the devices and its drivers.
4. The kernel mounts the root filesystem.
5. The kernel starts a program called init with a process ID of 1. This point is the user space start.
6. init sets the rest of the system processes in motion.
7. At some point, init starts a process allowing you to log in, usually at the end or near the end of the boot.

The kernel logs quite a bit of information at boot that can be invaluable for debugging. You can view some of these logs with `dmesg`

```bash
$ sudo dmesg | less # [j] to scroll down - [ctrl+c] to quit
```

When running the Linux Kernel, the bootloader passes a set of **kernel parameters** that tell how the kernel should start.

```bash
$ cat /proc/cmdline
BOOT_IMAGE=/vmlinuz-5.19.0-29-generic root=/dev/mapper/ubuntu--vg-ubuntu--lv ro
```