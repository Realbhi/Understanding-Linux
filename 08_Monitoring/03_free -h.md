Good, let’s switch cleanly to `free -h`.

---

## What does `free` do (one line)

> **`free` shows how system memory (RAM and swap) is being used right now.**

It answers:

* How much RAM do I have?
* How much is used?
* How much is actually available?
* How much swap is used?

---

## What does `-h` mean?

```bash
free -h
```

### `-h` = **human-readable**

It tells `free` to:

* show sizes in **KB / MB / GB**
* instead of raw bytes

Example:

Without `-h`:

```
Mem:   16344956  8234560  10240  ...
```

With `-h`:

```
Mem:      15Gi     7.8Gi    10Mi ...
```

Same data — just easier to read.

---

## Why `-h` matters

Memory numbers are big.

Humans think in:

* MB
* GB

Machines think in:

* bytes

`-h` bridges that gap.

---

## Typical `free -h` output (what it means)

```
              total   used   free   shared   buff/cache   available
Mem:           15Gi   7Gi    500Mi  200Mi        7.5Gi        7.2Gi
Swap:           2Gi   0B       2Gi
```

### Key columns (important)

* **total** → total RAM
* **used** → memory used by processes (not cache)
* **free** → completely unused RAM
* **buff/cache** → memory used for filesystem cache
* **available** → memory available for new apps *without swapping*
* **swap** → disk-backed memory

---

## The most misunderstood column (very important)

### `free` ≠ “usable memory”

Then why does free exist at all?

free exists because:

- it is a low-level metric

- it tells the kernel how much memory is instantly unused

- it is useful for kernel developers and debugging

But for humans and admins, it is misleading if used alone.

Linux **intentionally uses RAM** for caching.

So:

* low `free` is normal
* **`available` is what you care about**

available = free + reclaimable cache + reclaimable buffers

That’s why:
```
available  >> free
```

Example:

free       = 500MB
available  = 7.2GB

---

## One-sentence mental model (lock this in)

> **`free -h` shows how much RAM you have, how much is really available, and whether the system is swapping — in human-readable units.**

---



