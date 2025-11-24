#  **Goal**

You want:

* You still connect to the VM (EC2)
* But instead of logging in as `ubuntu` or `ec2-user` with the `.pem`
* You want to log in as **xyz**, using **xyz’s own SSH key**

Perfect — here is the right sequence.

---

#  Step 1: Create the user on the VM (if not already created)

On the VM (logged in as ubuntu with your .pem):

```
sudo adduser xyz
```

Or:

```
sudo useradd -m -s /bin/bash xyz
sudo passwd xyz
```

Then:

```
sudo su - xyz
```

---

#  Step 2: Generate SSH key **on your local machine** (NOT inside the VM)

On your **local laptop/desktop**, run:

```
ssh-keygen -t ed25519 -C "xyz@yourmachine"
```

This will create:

```
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

 **Never send the private key (`id_ed25519`) to the server. Only the `.pub` file goes to the VM.**

---

#  Step 3: Copy public key to VM under user xyz

You have two options:

##  Option 1: Using ssh-copy-id (easy, if available):

```
ssh-copy-id -i ~/.ssh/id_ed25519.pub xyz@server-ip
```

If this doesn’t work, use Option 2.

---

##  Option 2: Copy manually

### 1. On your local system, show the public key:

```
cat ~/.ssh/id_ed25519.pub
```

Copy the output.

### 2. SSH into VM using the `.pem`:

```
ssh -i mykey.pem ubuntu@server-ip
```

### 3. Switch to user xyz:

```
sudo su - xyz
```

### 4. Create .ssh directory:

```
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

### 5. Create authorized_keys file and paste your key:

```
nano ~/.ssh/authorized_keys
```

Paste the public key you copied.

Save file.

### 6. Set correct permissions:

```
chmod 600 ~/.ssh/authorized_keys
chown -R xyz:xyz ~/.ssh
```

---

#  Step 4: SSH as xyz from your local machine

```
ssh -i ~/.ssh/id_ed25519 xyz@server-ip
```

Or if your key is default:

```
ssh xyz@server-ip
```

---

#  Note About AWS EC2 & .pem Login

Your `.pem` file is only used for the **default user** created by AWS (usually `ubuntu`, `ec2-user`, or `centos`).
For any new user you create:

* They must have their **own** key.
* You must create and set up their `authorized_keys` manually.


