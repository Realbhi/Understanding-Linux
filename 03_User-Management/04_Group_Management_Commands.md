# Working with Groups in Linux

Groups in Linux are a way to organize users so they can share permissions and access to files or resources.
Each user belongs to:

* **One primary group** (main group assigned at user creation), and
* **Zero or more supplementary (secondary) groups.**

Group data is stored in `/etc/group`.

---

## **1. Creating Groups**

### **Command:**

```bash
groupadd groupname
```

### **Explanation:**

* Creates a new **group entry** in the system.
* Assigns a unique **Group ID (GID)** automatically.
* The new group is recorded in `/etc/group`.

Example:

```bash
sudo groupadd developers
```

Now check:

```bash
cat /etc/group | grep developers
```

Output:

```
developers:x:1002:
```

| Field        | Meaning                                  |
| ------------ | ---------------------------------------- |
| `developers` | Group name                               |
| `x`          | Placeholder (password info, rarely used) |
| `1002`       | Group ID (GID)                           |
| *(empty)*    | List of members in this group            |

---

## **2. Finding Group Information**

### **Command:**

```bash
cat /etc/group
```

### **Explanation:**

* Displays all groups defined on the system.
* Each line represents one group in the format:

```
group_name:x:GID:user1,user2,user3
```

Example:

```
root:x:0:
sudo:x:27:ubuntu
developers:x:1002:ash
```

| Field          | Description                                          |
| -------------- | ---------------------------------------------------- |
| **group_name** | The name of the group                                |
| **x**          | Placeholder for encrypted password (rarely used now) |
| **GID**        | Numeric Group ID                                     |
| **user list**  | Comma-separated list of users in the group           |

---

## **3. Adding Users to Groups**

### **Command:**

```bash
usermod -aG groupname username
```

### **Explanation:**

* Adds an existing user to a **supplementary (secondary) group**.
* `-a` = append (without removing from other groups)
* `-G` = specify the group(s) to add

Example:

```bash
sudo usermod -aG developers ash
```

This makes user **ash** a member of **developers**.

**NOTE ::**  If you forget `-a`, it **removes all other group memberships** and replaces them with only the specified group.

To confirm:

```bash
groups ash
```

---

## **4. Viewing Group Memberships**

### **Command:**

```bash
groups username
```

### **Explanation:**

Displays all groups that a user belongs to.

Example:

```bash
groups ash
```

Output:

```
ash : ash sudo developers docker
```

* The **first** group (`ash`) is the **primary group**.
* The rest (`sudo`, `developers`, `docker`) are **secondary groups**.

---

## **5. Changing a User’s Primary Group**

### **Command:**

```bash
usermod -g new_primary_group username
```

### **Explanation:**

Changes the user’s **primary group**.

Example:

```bash
sudo usermod -g developers ash
```

Now, the user’s **primary group** becomes `developers`.

Check:

```bash
id ash
```

Output:

```
uid=1001(ash) gid=1002(developers) groups=1002(developers),27(sudo),999(docker)
```

| Field                  | Meaning                     |
| ---------------------- | --------------------------- |
| `gid=1002(developers)` | Primary group               |
| `groups=`              | Lists all group memberships |

> When you create files, their **group ownership** defaults to your primary group.

---

## **6. Important Group Files**

| File           | Purpose                                                      |
| -------------- | ------------------------------------------------------------ |
| `/etc/group`   | Defines all groups and their members.                        |
| `/etc/gshadow` | Stores secure group-related info (like passwords or admins). |
| `/etc/passwd`  | Shows each user’s primary group ID.                          |

---

## **7. Useful Verification Commands**

| Command                  | Purpose                                           |
| ------------------------ | ------------------------------------------------- |
| `groups`                 | Shows groups for current user                     |
| `groups username`        | Shows groups for a specific user                  |
| `id username`            | Shows UID, primary GID, and all group memberships |
| `getent group groupname` | Prints info about a specific group                |

---

###  Notes:

* **Primary group:** Every file a user creates belongs to their primary group.
* **Secondary groups:** Provide additional access privileges (e.g., joining `sudo` or `docker` groups).
* Always use `-aG` (append + groups) to avoid overwriting memberships.
* To make group changes effective immediately, the user can **log out and back in**, or use:

  ```bash
  newgrp groupname
  ```




