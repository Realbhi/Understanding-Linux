### Demonstration of Default File Permissions Using Multiple Users

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
