## Viewing Process Details
---

### Using `ps`

Show processes for a specific user:

```bash
ps -u username
```
---

Show a process by name:

```bash
ps -C processname
```

To know what value can be used as <processname> for
ps -C <processname> (on Linux),

**inspect the comm column.**

And the reliable way to see that is:
```
ps -eo pid,comm,args
```

**-e :**
Select every process on the system

Without -e, ps would only show processes tied to the current terminal.


**-o :**
Custom output format

It tells ps:
“Only show the columns I explicitly ask for, in this exact order.”

---

### Using `pgrep`

Find a process by name and return its PID:

```bash
pgrep processname
```

---

### Using `pidof`

Find the PID of a running program:

```bash
pidof processname
```
