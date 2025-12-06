## **Sudoers: Granting Command Access to Multiple Users**

In the `/etc/sudoers` file, permissions are assigned per user. A typical rule looks like:

```
username ALL=(ALL) /path/to/command
```

**Meaning:**

* `username` → who can run the command
* `ALL` → allowed from any host
* `(ALL)` → can run the command as any target user (including root)
* `/path/to/command` → the exact command allowed with sudo

## 

**To grant the **same permission to multiple users**, there are two valid methods**:

### **1. Separate rules (clear and simple)**

```
ash  ALL=(ALL) /usr/bin/systemctl restart nginx, /usr/bin/systemctl restart apache2
ash1 ALL=(ALL) /usr/bin/systemctl restart nginx, /usr/bin/systemctl restart apache2
```

### **2. Combined rule (compact)**

```
ash, ash1 ALL=(ALL) /usr/bin/systemctl restart nginx, /usr/bin/systemctl restart apache2
```

Both give identical permissions.
Use **separate lines** for readability, or **combined lines** to avoid repetition.

### **Recommended for many users:** Use a sudoers alias

```
User_Alias WEBADMINS = ash, ash1, ash2
WEBADMINS ALL=(ALL) /usr/bin/systemctl restart nginx, /usr/bin/systemctl restart apache2
```

This keeps the file clean and scalable — just add new usernames to the alias.

