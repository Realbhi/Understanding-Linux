## ** The Command Prompt and User Context**

When logged into a Linux terminal, the **prompt** provides key information about who you are, where you are, and what permissions you have.

###  Structure:

```
user@hostname:path$
```

or

```
user@hostname:path#
```

| Component          | Meaning                                                            |
| ------------------ | ------------------------------------------------------------------ |
| **user**           | The current logged-in user (e.g., `root`, `ubuntu`, `ash`).        |
| **hostname**       | The name of the machine on a network (set by the OS or container). |
| **path**           | The current working directory — your location in the filesystem.   |
| **symbol (# / $)** | `#` means root (superuser); `$` means a normal user.               |

###  Example:

```
root@ubuntu-dev:/home/ubuntu#
```

* `root`: You’re logged in as the superuser.
* `ubuntu-dev`: The system or container’s hostname.
* `/home/ubuntu`: Current directory.
* `#`: Indicates administrative privileges.

###  Home directory shorthand:

* `~` refers to the current user’s home directory.

  * For user `ubuntu`: `~` → `/home/ubuntu`
  * For user `root`: `~` → `/root` (note: root’s home is directly under `/`)

Understanding these elements helps orient you within the Linux filesystem and recognize your permission level.


