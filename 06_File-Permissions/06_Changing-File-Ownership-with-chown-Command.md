### The chown command changes the ownership of files or directories:
---

**Ownership consists of the user owner and the group owner.**

```
Syntax: chown user:group filename
```

**Only the root user can change ownership.**
---


**Use case example:**

A developer creates a file but wants to transfer management to QE.
Root executes chown qe:qe test.sh to transfer ownership.


**Key Points:**
```
Ownership and permissions are distinct but related.
Ownership controls who can modify permissions and who is considered the file owner.
Permissions control what the owner, group, and others can do with the file.```
