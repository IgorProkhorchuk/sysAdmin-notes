Mounting attaches a file system to a specific location in the directory tree, allowing access to its contents. Unmounting detaches the file system, ensuring any pending data writes are completed and the device is safely disconnected.

---

## **1. Mounting File Systems**

### What is Mounting?

Mounting is the process of making a file system accessible at a certain point in the directory hierarchy. This mount point is an empty directory (or an already mounted location) where the contents of the file system become available.

For example, if you insert a USB drive or attach a new partition, you must mount it to access its files. Until the file system is mounted, you cannot interact with its contents.

### Common Mount Points
- **Root (`/`)**: The root file system is mounted at boot time, where the entire directory hierarchy begins.
- **User Data Mount Points**: Partitions for user data, such as `/home` for user home directories, or `/media` and `/mnt` for external storage like USB drives.

### Steps for Mounting a File System

#### 1.1. **Identify the Device**

Before mounting, identify the device you want to mount using `lsblk`, `fdisk`, or `blkid`. These commands will show the available storage devices and partitions.

```bash
$ lsblk
```

Example output:

```
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0  256G  0 disk 
├─sda1   8:1    0  512M  0 part /boot/efi
├─sda2   8:2    0   1G   0 part /boot
└─sda3   8:3    0 254.5G 0 part /
sdb      8:16   1   32G  0 disk 
└─sdb1   8:17   1   32G  0 part
```

Here, `/dev/sdb1` is a 32GB partition, which is likely an external storage device.

#### 1.2. **Create a Mount Point**

To mount a file system, you need to designate an empty directory as the mount point. You can either use a pre-existing directory like `/mnt` or `/media` or create a new one.

```bash
$ sudo mkdir /mnt/myusb
```

This command creates a directory called `myusb` in `/mnt`, which will serve as the mount point.

#### 1.3. **Mount the File System**

Use the `mount` command to mount the device at the desired mount point. The basic syntax is:

```bash
$ sudo mount <device> <mount-point>
```

For example, to mount the `sdb1` partition to `/mnt/myusb`:

```bash
$ sudo mount /dev/sdb1 /mnt/myusb
```

#### 1.4. **Verify the Mount**

You can verify that the file system has been successfully mounted using the `df` or `mount` command:

```bash
$ df -h
```

Example output:

```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3       254G   15G  227G   7% /
/dev/sdb1        32G   10G   22G  30% /mnt/myusb
```

Here, `/dev/sdb1` is successfully mounted at `/mnt/myusb`.

---

## **2. Unmounting File Systems**

### What is Unmounting?

Unmounting a file system detaches it from the directory hierarchy, ensuring all pending write operations to the storage device are completed before removal. It is critical to unmount devices, like USB drives or network shares, to avoid data corruption or loss.

### Steps for Unmounting a File System

#### 2.1. **Unmount the File System**

To unmount a file system, use the `umount` command. You can specify either the device or the mount point. The syntax is:

```bash
$ sudo umount <device-or-mount-point>
```

For example, to unmount `/mnt/myusb`:

```bash
$ sudo umount /mnt/myusb
```

Alternatively, you can unmount it by referencing the device:

```bash
$ sudo umount /dev/sdb1
```

#### 2.2. **Verify the Unmount**

To check if the file system has been successfully unmounted, you can use the `df` command again or list the currently mounted file systems:

```bash
$ df -h
```

If `/mnt/myusb` is no longer listed, the unmount operation was successful.

You can also use the `mount` command to list currently mounted file systems:

```bash
$ mount | grep /mnt/myusb
```

If nothing is returned, the device has been unmounted.

---

## **3. Mounting File Systems at Boot Time (Permanent Mounts)**

For file systems that need to be mounted automatically at boot time (such as separate `/home` partitions or external drives), you can add entries to the `/etc/fstab` file.

### **Understanding `/etc/fstab`**

The `/etc/fstab` file contains a list of file systems that are mounted during the boot process. Each line in this file describes a file system, with information on:
- The device
- The mount point
- The file system type (e.g., `ext4`, `xfs`, `vfat`)
- Mount options
- Dump and fsck options

### Example `/etc/fstab` Entry:

```bash
/dev/sdb1   /mnt/myusb   ext4    defaults   0  0
```

This entry specifies that:
- `/dev/sdb1` (the device) should be mounted at `/mnt/myusb` (the mount point).
- The file system type is `ext4`.
- The mount options are `defaults` (read/write, with other standard options).
- The `0 0` at the end indicates that the dump and fsck checks are disabled.

To add a new device to be mounted at boot:
1. Open the `/etc/fstab` file for editing (using a text editor like `nano` or `vim`).
2. Add a new line for the device and its mount point.
3. Save the file and exit.

#### Testing `/etc/fstab` Without Rebooting

You can use the `mount -a` command to apply the changes in `/etc/fstab` without rebooting:

```bash
$ sudo mount -a
```

This command mounts all file systems listed in `/etc/fstab` that are not already mounted.

---

## **4. Advanced Mounting Options**

### 4.1. **Mounting with Specific File System Types**

If the device has a specific file system (e.g., `ext4`, `xfs`, `vfat`), you can explicitly specify the type when mounting:

```bash
$ sudo mount -t ext4 /dev/sdb1 /mnt/myusb
```

This is useful when the system cannot automatically detect the file system type.

### 4.2. **Read-Only Mount**

Sometimes you may want to mount a file system in read-only mode, either to prevent accidental changes or if the file system is corrupted.

```bash
$ sudo mount -o ro /dev/sdb1 /mnt/myusb
```

This ensures that no data can be written to the file system while it is mounted.

### 4.3. **Mounting Network File Systems**

You can also mount network file systems like NFS or SMB (Samba) shares. For example, to mount an NFS share:

```bash
$ sudo mount -t nfs server:/path/to/share /mnt/mynfs
```

For Samba shares (Windows shares), use:

```bash
$ sudo mount -t cifs //server/share /mnt/mysamba -o username=user,password=pass
```

---

## **5. Troubleshooting Mounting Issues**

### 5.1. **File System Not Found**

If you try to mount a device and receive a "file system not found" error, check if the correct device path is being used. Also, verify the file system type using `blkid`:

```bash
$ sudo blkid /dev/sdb1
```

This command will show the file system type, allowing you to mount it with the correct type (e.g., `ext4`, `vfat`, `ntfs`).

### 5.2. **Busy Device**

When attempting to unmount a file system, you may receive a "device is busy" error. This indicates that some process is still using the file system. You can find the culprit using:

```bash
$ sudo lsof +f -- /mnt/myusb
```

This command lists open files on the device. You can then close those processes or stop using the file system to allow for unmounting.

---

## **6. Automounting with `systemd`**

In modern Linux systems, `systemd` can be used for automounting devices. You can create a unit file to define automount points and options.

### Example Automount Unit File:

```bash
[Unit]
Description=Automount USB Drive

[Mount]
What=/dev/sdb1
Where=/mnt/myusb
Type=ext4
Options=defaults

[Install]
WantedBy=multi-user.target


```

---

