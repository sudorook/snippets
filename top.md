# `top`

(consider merging with `ps` into `procps-ng` document)

Let's go over what this output means, you don't have to memorize this, but come
back to this when you need a reference.

1st line: This is the same information you would see if you ran the uptime
command (more to come)

The fields are from left to right:

1. Current time
2. How long the system has been running
3. How many users are currently logged on
4. System load average (more to come)

2nd line: Tasks that are running, sleeping, stopped and zombied

3rd line: Cpu information

1. us: user CPU time - Percentage of CPU time spent running users\u2019
   processes that aren\u2019t niced.
2. sy: system CPU time - Percentage of CPU time spent running the kernel and
   kernel processes
3. ni: nice CPU time - Percentage of CPU time spent running niced processes
4. id: CPU idle time - Percentage of CPU time that is spent idle
5. wa: I/O wait - Percentage of CPU time that is spent waiting for I/O. If this
   value is low, the problem probably isn\u2019t disk or network I/O
6. hi: hardware interrupts - Percentage of CPU time spent serving hardware
   interrupts
7. si: software interrupts - Percentage of CPU time spent serving software
   interrupts
8. st: steal time - If you are running virtual machines, this is the percentage
   of CPU time that was stolen from you for other tasks

4th and 5th line: Memory Usage and Swap Usage

Processes List that are Currently in Use

1. PID: Id of the process
2. USER: user that is the owner of the process
3. PR: Priority of process
4. NI: The nice value
5. VIRT: Virtual memory used by the process
6. RES: Physical memory used from the process
7. SHR: Shared memory of the process
8. S: Indicates the status of the process: S=sleep, R=running,
   Z=zombie,D=uninterruptible,T=stopped
9. %CPU - this is the percent of CPU used by this process
10. %MEM - percentage of RAM used by this process
11. TIME+ - total time of activity of this process
12. COMMAND - name of the process

You can also specify a process ID if you just want to track certain processes:

```sh
top -p <pid>
```
