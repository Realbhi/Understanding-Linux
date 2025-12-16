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

- All processes from all users
- Including background services and daemons
- Not limited to any terminal

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
ps - ef
```
---

Counting processes can be done using pipe commands such as :
```
ps aux | nl or ps aux | wc -l.
```
