### Understanding Syntax :

A central concept in Linux file permissions is the 10-character string shown by ls -l that encodes file type and access rights. For example:
```-rw-rw-r--```

**This string breaks down as follows:**

**The first character indicates file type:**
```
- for regular file
d for directory
```

**The next nine characters are split into three groups of three:**
```
User (owner) permissions (first three)
Group permissions (middle three)
Others permissions (last three)
```

**Each group represents permissions for:**
```
Read ®: Ability to view the contents
Write (w): Ability to modify or delete
Execute (x): Ability to run a file (e.g., shell scripts or programs) or enter a directory
```
```
For example, rw- means read and write permissions, but no execute permission.
```

**Explanation of Parties:**
```
User (u): The owner of the file, usually the creator.
Group (g): A collection of users who share similar access rights.
Others (o): All other users not in the user or group categories.
```

**Example:**
```
-rw-rw-r--

- User has read and write permissions.
- Group has read and write permissions.
- Others have read-only permission.
```
