here is a **clear, accurate, step-by-step explanation of each command** involved in preparing a newly attached disk/volume on Linux.

---

#  1. `lsblk`

### **Command**

```bash
lsblk
```

### **What it does**

* Lists **all block devices** (disks, volumes, partitions).
* Shows device names like `/dev/sda`, `/dev/xvdf`, `/dev/nvme1n1`.
* Shows size, type, and mount points.

### **Why you use it**

* To check whether the new volume has been detected.
* To see if it has partitions or a filesystem already.

---

#  2. `fdisk /dev/xvdf` (or any disk)

### **Command**

```bash
fdisk /dev/xvdf
```

### **What it does**

* Opens the **fdisk utility** for partitioning the disk.
* Lets you create partitions such as `/dev/xvdf1`.

### **Common steps inside fdisk**

* Press `n` → create a new partition
* Press `w` → write changes to disk

### **Why you use it**

* To create a partition table on the new raw disk.
* This step is optional — you can format the entire disk directly — but partitioning is more standard.

---

#  3. `mkfs.ext4 /dev/xvdf1`

### **Command**

```bash
mkfs.ext4 /dev/xvdf1
```

### **What it does**

* **Formats** the partition with the EXT4 filesystem.
* Creates the filesystem metadata, directory structures, etc.

### **Alternate command**

```bash
mkfs.xfs /dev/xvdf1
```

(xfs is often used for databases or large storage)

### **Why you use it**

* No disk can be mounted or used until it has a filesystem.
* This prepares the partition for use by Linux.

---

#  4. `mkdir /mnt/data` (example)

### **Command**

```bash
mkdir /mnt/data
```

### **What it does**

* Creates an **empty directory** to use as a mount point.

### **Why you use it**

* A filesystem can only be mounted onto a directory.
* `/mnt`, `/data`, `/disk`, or `/mnt/data` are common choices.

---

#  5. `mount /dev/xvdf1 /mnt/data`

### **Command**

```bash
mount /dev/xvdf1 /mnt/data
```

### **What it does**

* Mounts the formatted filesystem onto the directory.
* Makes the disk accessible at `/mnt/data`.

### **Why you use it**

* Before mounting, the volume is not usable.
* After mounting, applications can read/write into the mount point directory.

---

#  6. `df -h`

### **Command**

```bash
df -h
```

### **What it does**

* Shows mounted filesystems, their sizes, and usage.
* `-h` = human-readable sizes (GB, MB).

### **Why you use it**

* To confirm the new disk is mounted properly.

---

#  7. Add entry to `/etc/fstab` (optional but recommended)

### **Example entry**

```
/dev/xvdf1  /mnt/data  ext4  defaults,nofail  0  2
```

### **What it does**

* Configures the system to mount the disk automatically on boot.

### **Why you use it**

* Without this, the mount disappears after reboot.
* With fstab, the disk is always available.

---

