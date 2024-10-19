The `fdisk` tool is one of the most widely used command-line utilities in Linux and Unix-like systems for managing disk partitions. It's a powerful tool for creating, deleting, resizing, and organizing partitions on a hard disk. Despite the increasing popularity of more modern tools like `gdisk` (for GPT partitions) or `parted`, `fdisk` remains a fundamental and accessible option for managing MBR and GPT disk partitions.

In this explanation, we'll cover the following topics in detail:
1. What `fdisk` is and how it works
2. Partitioning basics
3. Practical tasks and commands
4. Understanding the output of `fdisk`
5. Partition types (`MBR` vs. `GPT`)
6. Example use cases
7. Common `fdisk` commands

---

## **1. What is `fdisk`?**

`fdisk` stands for **fixed disk** and is a disk partitioning utility available on Linux and other Unix-like operating systems. It operates directly on the partition table, allowing users to modify the layout of partitions on storage devices.

- **Key Features of `fdisk`:**
  - Creating new partitions
  - Deleting partitions
  - Viewing partition information
  - Setting partition types (like Linux, swap, NTFS)
  - Changing partition flags (such as making a partition bootable)
  - Writing partition table changes to the disk

### Warning: `fdisk` Modifies Disk Data!
Working with `fdisk` directly affects your disk’s partition table. If used improperly, it could lead to data loss. Always back up important data before making any modifications.

---

## **2. Understanding Disk Partitions**

Before diving into `fdisk`, it’s essential to understand what partitions are and their role in managing disk storage.

- **Disk Partition**: A disk can be divided into multiple sections called partitions. Each partition can function as an independent file system. 
- **Partition Table**: This is a structure that stores information about how a disk is partitioned. It is stored in the first sector of the disk.
- **Types of Partitions**:
  - **Primary Partition**: A disk can have up to 4 primary partitions with an MBR partition table. These are the main partitions for storing data.
  - **Extended Partition**: To overcome the 4 primary partition limit in MBR, one of the primary partitions can be designated as an extended partition. This extended partition can contain multiple **logical partitions**.
  - **Logical Partition**: Partitions within an extended partition, allowing you to have more than 4 partitions on an MBR disk.

---

## **3. Practical Tasks with `fdisk`**

Let's walk through some common tasks using `fdisk`.

### 3.1 **Listing Partitions**

To view the partition table of a disk, use the `-l` option:

```bash
$ sudo fdisk -l /dev/sda
```

This lists all partitions and their details on the `/dev/sda` disk (your main disk). If no disk is specified, it lists partitions on all available disks.

**Output Example**:
```
Disk /dev/sda: 256 GB, 256060514304 bytes, 500118192 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000

Device    Boot      Start         End      Blocks   Id  System
/dev/sda1 *          2048     1050623      524288   83  Linux
/dev/sda2         1050624   500117503   249533440   8e  Linux LVM
```

In this output:
- `/dev/sda1` is a Linux partition that is bootable (`*` under Boot).
- `/dev/sda2` is an LVM partition, used by Linux for logical volume management.

### 3.2 **Starting `fdisk` for a Specific Disk**

To begin partitioning a specific disk, run:

```bash
$ sudo fdisk /dev/sda
```

This opens `fdisk` in interactive mode for the `/dev/sda` disk. Once inside, `fdisk` provides an interactive command prompt where you can enter commands.

### 3.3 **Viewing Help Inside `fdisk`**

Once you’re inside `fdisk`, press `m` to view a list of available commands:

```bash
Command (m for help): m
```

This will display a list of commands like:
- `p` — Print the partition table
- `n` — Create a new partition
- `d` — Delete a partition
- `w` — Write the changes to disk and exit
- `q` — Quit without saving changes

### 3.4 **Creating a New Partition**

To create a new partition:

1. Start `fdisk` on your target disk:
   ```bash
   $ sudo fdisk /dev/sdb
   ```
   
2. Press `n` to create a new partition.

3. Choose between a **primary** or **extended** partition:
   ```
   Command action
      p   primary (1-4)
      e   extended
   ```

4. Select the partition number (e.g., 1 for `/dev/sdb1`).

5. Choose the starting sector (press **Enter** to select the default value).

6. Choose the partition size (e.g., `+10G` for a 10GB partition, or press **Enter** to use the remaining space).

7. After setting the size, the new partition is created but not yet saved. You must write the changes using the `w` command:
   ```bash
   Command (m for help): w
   ```

8. Once written, the changes take effect, and you can use `mkfs` to format the partition.

### 3.5 **Formatting the Partition**

After creating a partition, you must format it with a file system like `ext4`, `xfs`, or `vfat`:

```bash
$ sudo mkfs.ext4 /dev/sdb1
```

This command formats `/dev/sdb1` as an `ext4` file system.

### 3.6 **Deleting a Partition**

If you want to delete a partition:

1. Start `fdisk` on the desired disk.
   
2. Press `d` to delete a partition.
   
3. Enter the partition number (e.g., `1` to delete `/dev/sdb1`).

4. Write the changes with the `w` command to finalize the deletion.

---

## **4. Understanding the Output of `fdisk -l`**

The `fdisk -l` command lists the partition table for a disk. Let’s break down the fields:

```
Device    Boot      Start         End      Blocks   Id  System
/dev/sda1 *          2048     1050623      524288   83  Linux
/dev/sda2         1050624   500117503   249533440   8e  Linux LVM
```

- **Device**: The name of the partition (e.g., `/dev/sda1`).
- **Boot**: An asterisk (`*`) indicates that this partition is bootable.
- **Start/End**: These columns list the starting and ending sectors of the partition.
- **Blocks**: This shows the size of the partition in 1K blocks.
- **Id**: The partition type code (e.g., `83` is a Linux partition, `8e` is LVM).
- **System**: Describes the partition type (e.g., Linux, Linux LVM, swap, NTFS).

---

## **5. Partition Types: MBR vs. GPT**

There are two main types of partition tables: **MBR (Master Boot Record)** and **GPT (GUID Partition Table)**.

- **MBR**:
  - Old standard.
  - Supports up to 4 primary partitions.
  - Maximum disk size of 2TB.
  - Limited flexibility (requires extended/logical partitions for more than 4 partitions).
  
- **GPT**:
  - Modern standard (used with UEFI systems).
  - Supports virtually unlimited partitions (128 by default).
  - Can handle disks larger than 2TB.
  - Provides redundancy by storing multiple copies of the partition table.

To create or manage GPT partitions, use `gdisk` or specify the partition type when creating partitions with `fdisk`.

---

## **6. Example Use Cases for `fdisk`**

### **6.1. Resize a Partition**
1. Unmount the partition.
2. Delete it with `fdisk`.
3. Recreate it with the new size.
4. Resize the file system using `resize2fs` (for `ext4`).

### **6.2. Add a Swap Partition**
1. Create a new partition using `fdisk`.
2. Set its type to `82` (Linux swap).
3. Format it as a swap partition:
   ```bash
   $ sudo mkswap /dev/sdb2
   ```
4. Activate the swap partition:
   ```bash
   $ sudo swapon /dev/sdb2
   ```

---

## **7. Common `fdisk` Commands**

- **View partition table**: `sudo fdisk -l`
- **Start `fdisk` on a disk**: `sudo fdisk /dev/sda`
- **List available commands in `fdisk`**: Type `m`
- **Create a new partition**: Type `n`
- **Delete a partition**:

 Type `d`
- **Print partition table**: Type `p`
- **Write changes to disk**: Type `w`
- **Quit without saving changes**: Type `q`

---

## Summary

`fdisk` is a versatile and widely used tool for managing partitions in Linux. By understanding how it works and practicing with common tasks, you can confidently create, resize, and delete partitions on your system. However, because disk partitioning can lead to data loss if done incorrectly, it's always crucial to back up important data before making changes.
