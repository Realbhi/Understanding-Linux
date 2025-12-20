### Viewing Processes
---

Command is used to view running processes.
```
ps
```

Shows only:

- Processes owned by you
- Processes attached to the current terminal

Typical output:
```
PID
TTY
TIME
CMD
```

---

Lists all processes with detailed information including CPU and memory utilization.
```
ps aux
```
Shows:

- The ```a option``` displays processes from all users, not just the current user, lifting the restriction that normally limits the output to processes associated with the current terminal.
- The ```u option``` provides a user-oriented format, showing detailed information about each process, including the user who owns it, CPU and memory usage, and other relevant metrics.
- The ```x option``` includes processes that are not attached to a terminal (tty), such as background system services or daemons, which would otherwise be excluded from the output.

**Understanding ps aux Output**
```
- USER: The user who initiated the process.
- PID: Unique Process ID.
- CPU % and Memory %: Resource usage by the process.
- COMMAND: The command that started the process.
```
---
Lists processes but does not show memory utilization, only CPU usage.
```
ps -ef 
```
-e = select all processes (not just the ones attached to your terminal)
-f = full-format listing ( UID, PID,  PPID,  C, STIME, TTY, TIME, CMD )

```
ps -ef shows everything in a predefined full format,
ps -eo lets you choose exactly which columns to show.
```

---

Counting processes can be done using pipe commands such as :
```
ps aux | nl or ps aux | wc -l.
```

**ps aux | nl**
<img width="1428" height="618" alt="image" src="https://github.com/user-attachments/assets/db511273-ec91-4c2d-8c39-e247fd56c63b" />

**ps aux | wc -l**
<img width="1428" height="36" alt="image" src="https://github.com/user-attachments/assets/f84a836c-c989-42d7-9760-762625560e93" />


