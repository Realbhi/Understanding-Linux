# Monitoring System Processes

### View process priorities:

Using `top` 

```bash
top  # Look at the NI column
```

Interactive process viewer:

- Press `k` and enter a PID to kill a process.
- Press `r` to renice a process.
- Press `q` to quit.

---

### Using `htop`

A user-friendly alternative to `top`:

```bash
htop
```

Allows mouse-based interaction for process management.

---

### Using `nice` & `renice`

Run a command with a specific priority:

```bash
nice -n 10 command
```

Change the priority of an existing process:

```bash
renice -n -5 -p PID
```
