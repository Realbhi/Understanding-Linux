## Managing Processes
---

### Killing Processes

To terminate a process by PID:

```bash
kill PID
```
---

To terminate using process name:

```bash
pkill processname
```
---

Force kill a process:

```bash
kill -9 PID
```
---

Kill all instances of a process:

```bash
pkill -9 processname
```
---

### Stopping & Resuming Processes
---

Stop a running process:

```bash
kill -STOP PID
```
---

Resume a stopped process:

```bash
kill -CONT PID
```
