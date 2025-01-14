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
