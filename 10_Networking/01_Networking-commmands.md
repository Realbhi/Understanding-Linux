# Networking Commands

1. **`ping google.com`** – Checks connectivity to a remote server.
2. **`ifconfig`** – Displays network interfaces (deprecated, use `ip`).
3. **`ip a`** – Shows IP addresses of network interfaces.
4. **`netstat -tulnp`** – Displays open network connections.
5. **`curl https://example.com`** – Fetches a webpage's content.
6. **`wget https://example.com/file.zip`** – Downloads a file from the internet.


---


## `netstat` — *“What is happening on this machine?”*

### What `netstat` is used for

`netstat` **shows network state**, such as:

* Which **ports are open**
* Which **services are listening**
* Which **connections are active**
* Which **process is using which port** (on host systems)

So a clean statement is:

> **`netstat` shows what ports are open and what network connections are currently running on this machine.**

Example use cases:

* “Is my app listening on port 8080?”
* “Is anything already using port 3306?”
* “Do I have active connections to some server?”

---

##  `telnet` — *“Can I connect to that place?”*

### What `telnet` is used for

`telnet` is a **client tool** that tries to **connect to a host and port**.

It answers:

* “Can I reach this server?”
* “Is this port open and accepting connections?”

So a correct statement is:

> **`telnet` is used to test whether a connection to a remote host and port is possible.**

Example:

```bash
telnet google.com 80
telnet localhost 5432
```

If it connects → network + port are reachable
If it fails → firewall / service / network issue

---

##  Very important clarification (to avoid future confusion)

### `telnet` is NOT:

- ❌ A port scanner
- ❌ A security tool
- ❌ A modern protocol for real use

Today it is mostly used as a **connectivity tester**, not for actual communication.

---

##  Relationship between them (simple mental model)

* **`netstat`** → *observe*
* **`telnet`** → *test*

Or even simpler:

> **`netstat` looks inward, `telnet` reaches outward.**

---

##  Final corrected summary (perfect)

You can safely remember and say this:

> **`netstat` shows what ports are open and what connections exist on a system.
> `telnet` is used to check whether a connection to a host and port can be made.**

That’s **accurate, simple, and correct**.

---

### One small bonus (for later)

On modern Linux:

* `netstat` → replaced by `ss`
* `telnet` → often replaced by `nc` (netcat)


