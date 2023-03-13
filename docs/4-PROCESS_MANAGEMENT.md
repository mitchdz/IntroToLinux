# Process Management

Process management refers to the following actions of a process:

* Starting
* Pausing
* Resuming
* Terminating

---

You can view processes using a command such as 

```bash
$ top # use [Ctrl+c] to exit
# or
$ ps
```

(We will go more into reading `top` & `ps` later)

## Killing a process

To stop a process in Linux, you use the `kill` command, you can view all the signals by doing
```bash
$ kill -L
```
To stop a process, you send a signal (through `kill`) such as :
* signal 15, AKA **SIGTERM**
* signal 9 AKA **SIGKILL**.

To execute the kill command, you need the **PID** or Process ID. You can get the PID from both `top` & `ps`, for example you would execute

```bash
$ kill -SIGKILL 27707
# which is the same as
$ kill -9 27707
```

---

These processes by themselves are relatively straightforward and easy to do, however in real practice the kernel does a lot under the hood.

In real-world use-cases the kernel uses time-slicing for processes, this is how you can have many more processes than you have threads.

Time slicing is the process of running multiple processes "simultaneously" by context switching between them periodically.

A context switch does various things, here's a simple example:


1. The CPU (the actual hardware) interrupts the current process based on an internal timer, switches into
kernel mode, and hands control back to the kernel.
2. The kernel records the current state of the CPU and memory, which will be essential to resuming the
process that was just interrupted.
3. The kernel performs any tasks that might have come up during the preceding time slice (such as
collecting data from input and output, or I/O, operations).
4. The kernel is now ready to let another process run. The kernel analyzes the list of processes that are ready
to run and chooses one.
5. The kernel prepares the memory for this new process, and then prepares the CPU.
6. The kernel tells the CPU how long the time slice for the new process will last.
7. The kernel switches the CPU into user mode and hands control of the CPU to the process