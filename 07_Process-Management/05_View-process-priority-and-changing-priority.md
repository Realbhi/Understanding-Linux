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

---

## **More info :**

```bash
renice -n 5 -p PID
```

### What it does (Linux)

* Sets the **nice value** of the process with PID `PID` to **5**
* Nice range:

  * `-20` → highest priority
  * `0`   → default
  * `19`  → lowest priority
* `5` means **lower priority than normal**

---

### Important Linux rules

#### Increasing priority needs root

```bash
sudo renice -n -5 -p PID
```

####  Lowering priority does NOT need root

```bash
renice -n 10 -p PID
```

---

### Verify priority

```bash
ps -p PID -o pid,comm,ni
```

or with `top`:

* `NI` → nice value
* `PR` → scheduler priority (derived from nice)





