### Demonstration of Default File Permissions Using Multiple Users
---

**To illustrate file permissions in action, consider two users: developer and QE. Following steps demonstrate default permissions:
Create two users: developer and QE.**

- Log in as developer and create a script file hello_world.sh in the /tmp directory.
- Switch to QE user and observe:
  - QE can read the hello_world.sh file (cat hello_world.sh works).
  - QE cannot modify or delete the file; attempts to write or remove the file throw “operation not permitted” errors.
  
**This example confirms that by default:**

- Users can read files created by others.
- Users cannot modify or delete files they do not own.


**Key Points:**
```
Default Linux permissions allow read-only access to other users’ files.
Write and execute permissions are restricted to the file owner by default.
Permissions can be changed using the chmod command.
```

---

# How default permission works ?

---

Great question — and this is a **fundamental Linux concept**.
Let’s explain it cleanly and correctly.

---

#  **Do new files and folders get default permissions?**

**Yes.**
When you create a file or directory in Linux, it gets **default permissions** automatically.

BUT…
The permissions are not *fixed*. They depend on two things:

1. **The program creating the file** (e.g., `touch`, `mkdir`, editors, compilers)
2. **The user’s `umask` value**

---

#  1. Default permissions before applying `umask`

Linux has **base permissions** that programs use when creating files/directories:

### **For directories:**

```
777 (rwxrwxrwx)
```

### **For files:**

```
666 (rw-rw-rw-)
```

Why no execute (`x`) on files?
Because Linux **does not assume a new file is executable** unless you explicitly set it.

---

#  2. Then Linux applies the user’s `umask`

`umask` subtracts permissions from the default.

### See your umask:

```bash
umask
```

Typical values:

* `022` (most common)
* `002` (common for shared groups)
* `077` (secure/private)

### How umask works:

**Final permissions = Default permissions - Umask**

---

#  3. Example with umask 022

| Type      | Base | Umask 022 removes             | Final               |
| --------- | ---- | ----------------------------- | ------------------- |
| File      | 666  | remove write for group/others | **644** (rw-r--r--) |
| Directory | 777  | remove write for group/others | **755** (rwxr-xr-x) |

This is the most common case.

---

#  4. Example with umask 002 (common in developer groups)

| Type      | Base | Final               |
| --------- | ---- | ------------------- |
| File      | 666  | **664** (rw-rw-r--) |
| Directory | 777  | **775** (rwxrwxr-x) |

This allows members of the same group to write files.

---

#  5. Examples (real commands)

### **Create a file**

```bash
touch test.txt
ls -l test.txt
```

You’ll commonly see:

```
-rw-r--r-- 1 user user 0 date test.txt
```

### **Create a directory**

```bash
mkdir testdir
ls -ld testdir
```

You’ll commonly see:

```
drwxr-xr-x 2 user user 4096 date testdir
```

---

#  6. Are the permissions always the same?

Not always — it depends on **umask**.

### If umask is 022 → you get 644 files and 755 dirs

### If umask is 002 → you get 664 files and 775 dirs

### If umask is 077 → you get 600 files and 700 dirs

So **permissions can change** if:

* The user changes umask
* The shell changes it
* A service defines its own umask
* A program sets its own default

Example:

* Apache uses a special umask
* Systemd units can override umask

But **on a normal user session**, yes — permissions will be the same *every time* unless `umask` is modified.




