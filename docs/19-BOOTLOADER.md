# Bootloader

A bootloader is a low level piece of software that has a few tasks:

* Select among multiple kernels.
* Switch between sets of kernel parameters.
* Allow the user to manually override and edit kernel image names and parameters (for example, to enter single-user mode).
* Provide support for booting other operating systems.

A very common bootloader is **GRUB** or Grand Unified Bootloader.

You can view your current grub config like so:
```bash
$ cat /boot/grub/grub.cfg | less
```