# Device Files

Devices are very important in Linux as they are the way we interact with the hardware. Linux exposes access to devices in the form of **device files**.

To start, let's execute

```bash
$ echo "hello!" > /dev/null
```

The above command redirects the STDOUT to `/dev/null` which is a device file which the kernel simply ignores the input and throws away the data.

You can view your current devices with
```bash
$ ls -l /dev/
crw-r--r-- 1 root root     10, 235 Feb  1 20:12 autofs
drwxr-xr-x 2 root root         320 Mar  6 15:30 block
brw-rw---- 1 root disk      8,   0 Feb  1 20:12 sda
```

From the output of the above command, the first letter of each line is special and if it is either b, c, p, or s, the file is a device. These letters stand for block, character, pipe, and socket, respectively

* **Block device**  Programs access data from a block device in fixed chunks. The sda1 in the preceding example is a disk device, a type of block device. Disks can be easily split up into blocks of data. Because a block device’s total size is fixed and easy to index, processes have random access to any block in the device with the help of the kernel.
* **Character device** Character devices work with data streams. You can only read characters from or write characters to
character devices, as previously demonstrated with /dev/null. Character devices don’t have a size; when you
read from or write to one, the kernel usually performs a read or write operation on the device. Printers
directly attached to your computer are represented by character devices. It’s important to note that during
character device interaction, the kernel cannot back up and reexamine the data stream after it has passed
data to a device or process.
* **Pipe device** Named pipes are like character devices, with another process at the other end of the I/O stream instead of a
kernel driver.
Socket device
* **Sockets** are special-purpose interfaces that are frequently used for interprocess communication. They’re
often found outside of the /dev directory. Socket files represent Unix domain 

## dd
You will probably encounter the command `dd` in various guides, which is a very useful command when interacting with block and character devices.

```bash
$ dd if=/dev/zero of=new_file bs=1024 count=1
$ hexdump new_file
0000000 0000 0000 0000 0000 0000 0000 0000 0000
*
0000400
```

`dd` copies data in blocks of a fixed size. The above command uses `dd` with the character device `/dev/zero`.




You can view kernel events with

```bash
$ udevadm monitor --kernel
```