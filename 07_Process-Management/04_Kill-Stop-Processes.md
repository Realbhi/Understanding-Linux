## Managing Processes
---

### Killing Processes

To terminate a process by PID:

```bash
kill PID
```

- you are not killing the process directly.
- You are sending a signal to the process.
- The default signal is: SIGTERM (signal 15)

---

**If the process HAS a SIGTERM handler**

- Kernel delivers SIGTERM
- Handler runs
- Application decides what to do:
 - Clean up resources
 - Save state
 - Close connections

Then exit normally (usually via exit())

➡ This is called graceful termination
➡ The process chooses when and how to exit
➡ If it never exits, it can technically keep running

⚠️ Important:
A handler does not automatically kill the process.
The process must explicitly exit ie The process kills itself by calling exit().

##

**If the process does NOT have a SIGTERM handler**

- Kernel delivers SIGTERM
- Default action applies
- Kernel forcibly terminates the process
- No user-level code runs
 - Immediate termination
 - No graceful shutdown
 - Only kernel-level cleanup happens


---

**Does SIGTERM always terminate the process?**

- No ,  SIGTERM is a polite request: “Please stop yourself.”

- The process can:

  - obey it and exit (most do)

  - ignore it

  - catch it and clean up

  - delay termination

  - completely override the behavior

So SIGTERM does not guarantee termination. So we need to force kill which send SIGKILL (kill -9 PID)

**When SIGTERM is preferred**

Because SIGTERM gives the process a chance to:

- clean up files

- save data

- close connections

- release locks

Production services often rely on this.

---

To terminate using process name:

```bash
pkill processname
```

pkill processname does not use SIGKILL by default. pkill sends SIGTERM (signal 15) unless you specify another signal.

To force kill (SIGKILL), you must specify -9 **This also kills all instance of process**
```
pkill -9 processname
```

<img width="1460" height="540" alt="image" src="https://github.com/user-attachments/assets/a5bdfe26-6053-4b19-9031-feed0dd8fe30" />

---

Force kill a process:

```bash
kill -9 PID
```

- sends: SIGKILL (signal 9)

- SIGKILL:

  - cannot be ignored , caught and blocked

  - kills the process immediately at the kernel level

  - So yes, SIGKILL will terminate the process 100%, unless: process is in uninterruptible sleep state (D state), usually waiting on I/O.
 
  - In that case, even SIGKILL waits until the state clears.


---

### Stopping & Resuming Processes

Stop a running process:

```bash
kill -STOP PID
```

This signal (SIGSTOP) cannot be ignored, blocked, or handled by the process. It is enforced directly by the kernel.

So:

- The process immediately pauses

- It stops executing CPU instructions

- It remains in memory

- It stays visible in ps

This is why SIGSTOP is called a non-catchable, non-ignorable stop signal.

---

Resume a stopped process:

```bash
kill -CONT PID
```
- cant be prevented . Sends SIGCONT signal.
