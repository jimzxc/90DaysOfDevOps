## Linux process states (overview)

Linux commonly shows a process “state” using a single letter in tools like `ps` and `top`.

### Running / runnable (`R`)
- A new process may start in a running or runnable state.
- In this state, it is either currently executing on a CPU core or ready to run when scheduled.
- **Note**: tools often group *running* and *runnable* together as `R`.

### Sleeping (`S` and `D`)
There are two common sleeping states:

- **Interruptible sleep (`S`)**: the process is waiting and can be woken by signals and/or when a resource becomes available.
- **Uninterruptible sleep (`D`)**: the process is waiting on a resource (often I/O) and **does not react to signals** until the resource becomes available.

### Stopped (`T`)
A process can be stopped from the running/runnable state using signals:
- `SIGSTOP`: typically sent programmatically (example: `kill -STOP <pid>`). The process cannot ignore this signal.
- `SIGTSTP`: commonly sent interactively via `Ctrl + Z`.

### Zombie (`Z`)
- After a process exits, it may become a **zombie** (defunct) until its parent process reads its exit status.
- The child notifies the parent with `SIGCHLD`.
- The parent clears the child from the process table by calling `wait()` or `waitpid()`.

## Checking process state

### Using `ps`
Example output:

```text
PID     TTY  STAT   TIME    COMMAND
82863   s070 S      0:02.96 /Users/rsi-jimboy/.cache/gitstatus/gitstatusd-darwin-arm64 -G v1.5.4 -s -1 -u -1 -d -1 -c -1 -m -1 -v FATAL -t 22
93388   s070 T      0:00.14 gh auth login
95665   s073 Ss+    0:01.50 /bin/zsh -il
96163   s073 S      0:00.00 /bin/zsh -il
96165   s073 S      0:00.06 /bin/zsh -il
96167   s073 S      0:00.00 /bin/zsh -il
96172   s073 S      0:00.24 /Users/rsi-jimboy/.cache/gitstatus/gitstatusd-darwin-arm64 -G v1.5.4 -s -1 -u -1 -d -1 -c -1 -m -1 -v FATAL -t 22
96906   s079 Ss+    0:00.01 /bin/bash --init-file /Applications/Cursor.app/Contents/Resources/app/out/vs/workbench/contrib/terminal/common/scripts/shellIntegration-bash.sh
```

### Using `top`
`top` helps you see CPU usage and process state for running processes.

```text
Processes: 494 total, 4 running, 490 sleeping, 4798 threads                                                                                                                     17:21:53
Load Avg: 2.49, 2.95, 2.99  CPU usage: 7.31% user, 5.93% sys, 86.75% idle  SharedLibs: 573M resident, 120M data, 35M linkedit.
MemRegions: 1391224 total, 4531M resident, 82M private, 2969M shared. PhysMem: 17G used (3157M wired, 6615M compressor), 44M unused.
VM: 308T vsize, 4892M framework vsize, 107117205(0) swapins, 113415603(0) swapouts. Networks: packets: 77608034/63G in, 54383826/16G out.
Disks: 192244867/3628G read, 87878117/2513G written.

PID    COMMAND      %CPU TIME     #TH    #WQ  #PORTS MEM    PURG   CMPRS  PGRP  PPID  STATE    BOOSTS              %CPU_ME %CPU_OTHRS UID  FAULTS     COW       MSGSENT     MSGRECV
6845   pidinfo      27.7 00:00.37 5      4    25     4977K+ 0B     912K-  6845  1     sleeping *279+[3]            0.00000 27.18212   501  1238+      85        436+        374+
154    WindowServer 24.3 38:20:17 22/1   6    9202   1860M- 232M-  867M-  154   1     running  *0[1]               2.25430 0.95808    88   508900363+ 91726     1059837642+ 1932677450+
86759  iTerm2       18.1 02:44:10 8      5    387    411M-  165M+  90M-   86759 1     sleeping *0[11631]           27.6353 0.90216    501  116340836+ 434       38026496+   15197225+
0      kernel_task  11.3 70:45:47 581/11 0    0      36M+   0B     0B     0     0     running   0[0]               0.00000 0.00000    0    2711853    0         2110332354+ 1608597211+
```