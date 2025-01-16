# `ps`

## `ps aux` output

The output of `ps aux` is as follows:

- `USER`: effective user (the one whose access we are using)
- `PID`: process ID
- `%CPU`: CPU time used divided by the time the process has been running
- `%MEM`: ratio of the process's resident set size to the physical memory on the
  machine
- `VSZ`: virtual memory usage
- `RSS`: resident set size (the non-swapped physical memory that a task has
  used)
- `TTY`: controlling terminal associated with the process
- `STAT`: process status code
  - `R`: running or runnable, it is just waiting for the CPU to process it
  - `S`: Interruptible sleep, waiting for an event to complete, such as input
    from the terminal
  - `D`: Uninterruptible sleep, processes that cannot be killed or interrupted
    with a signal, usually to make them go away you have to reboot or fix the
    issue
  - `Z`: Zombie, we discussed in a previous lesson that zombies are terminated
    processes that are waiting to have their statuses collected
  - `T`: Stopped, a process that has been suspended/stopped
- `START`: start time of the process
- `TIME`: total CPU usage time
- `COMMAND`: name of executable/command

## Exit status

- `SIGHUP` or HUP or 1: Hangup
- `SIGINT` or INT or 2: Interrupt
- `SIGKILL` or KILL or 9: Kill
- `SIGSEGV` or SEGV or 11: Segmentation fault
- `SIGTERM` or TERM or 15: Software termination
- `SIGSTOP` or STOP: Stop

- `SIGHUP` - Hangup, sent to a process when the controlling terminal is closed.
  For example, if you closed a terminal window that had a process running in it,
  you would get a SIGHUP signal. So basically you've been hung up on
- `SIGINT` - Is an interrupt signal, so you can use Ctrl-C and the system will
  try to gracefully kill the process
- `SIGTERM` - Kill the process, but allow it to do some cleanup first
- `SIGKILL` - Kill the process, kill it with fire, doesn't do any cleanup
- `SIGSTOP` - Stop/suspend a process

## View all background jobs

```sh
jobs
```

To move current jobs to background, enter `CTRL+z`, and to restore it to the
foreground, run `fg`. `fg` will default to the most recently backgrounded
process, but to specify the process, use its job ID (from `jobs`, different from
process ID).

## View process threads

```sh
ps m
```

## `iostat` output

The first part is the CPU information:

1. `%user` - Show the percentage of CPU utilization that occurred while
   executing at the user level (application)
2. `%nice`- Show the percentage of CPU utilization that occurred while executing
   at the user level with nice priority.user CPU utilization with nice
   priorities
3. `%system` - Show the percentage of CPU utilization that occurred while
   executing at the system level (kernel).
4. `%iowait` - Show the percentage of time that the CPU or CPUs were idle during
   which the system had an outstanding disk I/O request.
5. `%steal` - Show the percentage of time spent in involuntary wait by the
   virtual CPU or CPUs while the hypervisor was servicing another virtual
   processor.
6. `%idle` - Show the percentage of time that the CPU or CPUs were idle and the
   system did not have an outstanding disk I/O request.

The second part is the disk utilization:

1. `tps` - Indicate the number of transfers per second that were issued to the
   device. A transfer is an I/O request to the device. Multiple logical requests
   can be combined into a single I/O request to the device. A transfer is of
   indeterminate size.
2. `kB_read/s` - Indicate the amount of data read from the device expressed in
   kilobytes per second.
3. `kB_wrtn/s` - Indicate the amount of data written to the device expressed in
   kilobytes per second.
4. `kB_read` - The total number of kilobytes read.
5. `kB_wrtn` - The total number of kilobytes written.
