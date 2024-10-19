The `parted` utility is a powerful, interactive, and command-line tool used in Linux to manage disk partitions. It is particularly useful for handling larger hard drives and offers support for a wide range of partition types, including **GPT** (GUID Partition Table) and **MBR** (Master Boot Record). `parted` can be used to create, resize, move, delete, and copy partitions and is favored for its flexibility in handling modern storage devices.

Unlike `fdisk`, which is mostly limited to MBR, `parted` fully supports both GPT and MBR, making it more suitable for larger disks (over 2 TB) and modern systems that require GPT partition tables. This tool is commonly used by system administrators and advanced users who need fine-grained control over disk partitions.

---

## **Key Features of `parted`**

1. **Support for Both GPT and MBR**: `parted` can handle both older and newer partitioning schemes, giving users flexibility when managing disks.
  
2. **Dynamic Partition Resizing**: It allows for resizing partitions without data loss (if done carefully and with supported filesystems), which can be useful for increasing storage space.

3. **Non-Interactive and Interactive Modes**: `parted` can be run interactively, where the user enters commands in a session, or non-interactively by specifying the commands directly in the terminal.

4. **Support for Modern Disks**: Handles disks over 2 TB in size, making it essential for managing large drives.

5. **Disk Alignment**: Automatically aligns partitions to the proper sector boundaries, which is important for performance in SSDs and newer hard drives.

---

## **Basic Syntax and Usage**

The basic syntax of `parted` is:

```bash
$ sudo parted [options] [device] [command]
```

For example, to start working with a specific disk, you can run:

```bash
$ sudo parted /dev/sda
```

### **Entering Interactive Mode**

In interactive mode, you’ll be presented with a `parted` prompt where you can issue commands directly. For example:

```bash
(parted) 
```

You can then use various commands such as `print`, `mklabel`, `mkpart`, and more.

### **Exiting Interactive Mode**

To exit the `parted` prompt, use the `quit` command:

```bash
(parted) quit
```

### **Non-Interactive Mode**

You can also pass commands directly to `parted` without entering interactive mode. For example:

```bash
$ sudo parted /dev/sda print
```

This will immediately print the partition table for `/dev/sda` without requiring an interactive session.

---

## **Common `parted` Commands and Options**

### 1. **Creating a New Partition Table (mklabel)**

Before partitioning a new disk, you must define a partition table format (GPT or MBR). To do this, you use the `mklabel` command.

For MBR:

```bash
(parted) mklabel msdos
```

For GPT:

```bash
(parted) mklabel gpt
```

### 2. **Displaying the Partition Table (print)**

To see the current partition table for a specific disk, use the `print` command:

```bash
(parted) print
```

Example output:

```
Model: ATA Samsung SSD (scsi)
Disk /dev/sda: 256GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 

Number  Start   End    Size    File system  Name     Flags
 1      1049kB  538MB  537MB   ext4         primary  boot
 2      538MB   256GB  255GB   ext4         primary
```

### 3. **Creating a Partition (mkpart)**

The `mkpart` command creates a partition with a specified filesystem type. You need to specify the partition type, start, and end points (in megabytes, gigabytes, etc.).

Example (creating an ext4 partition from 1GB to 50GB):

```bash
(parted) mkpart primary ext4 1GB 50GB
```

This creates a primary partition with an ext4 filesystem that starts at 1 GB and ends at 50 GB.

### 4. **Resizing a Partition (resizepart)**

Resizing a partition can be done using the `resizepart` command. Be cautious with resizing, especially if data is stored on the partition. The general syntax is:

```bash
(parted) resizepart [partition_number] [end_position]
```

Example:

```bash
(parted) resizepart 1 100GB
```

This command resizes the first partition (`1`) to end at the 100 GB mark.

### 5. **Removing a Partition (rm)**

To delete a partition, you can use the `rm` command followed by the partition number. This will remove the specified partition from the disk:

```bash
(parted) rm 2
```

This removes partition 2 from the disk.

### 6. **Checking Disk Alignment (align-check)**

Proper alignment of partitions is crucial for performance, especially on SSDs. To check whether a partition is aligned, you can use the `align-check` command:

```bash
(parted) align-check optimal [partition_number]
```

Example:

```bash
(parted) align-check optimal 1
```

This checks if the first partition is properly aligned.

### 7. **Setting Partition Flags (set)**

The `set` command allows you to enable or disable various partition flags, such as the **boot** flag (for making a partition bootable) or **lvm** for Logical Volume Manager. To set a flag, use:

```bash
(parted) set [partition_number] [flag] [on|off]
```

Example:

```bash
(parted) set 1 boot on
```

This makes the first partition bootable.

### 8. **Showing Partition Information (unit)**

By default, `parted` displays sizes in human-readable units, such as MB, GB, or TB. You can change the unit of measurement using the `unit` command. For example, to show sizes in sectors:

```bash
(parted) unit s
```

To go back to megabytes:

```bash
(parted) unit MB
```

### 9. **Partition Table Creation and Disk Formatting**

To format an entire disk, you first need to create a partition table with `mklabel`, then create partitions using `mkpart`, and finally, format each partition using a filesystem utility like `mkfs`. Example:

```bash
$ sudo parted /dev/sdb mklabel gpt
$ sudo parted /dev/sdb mkpart primary ext4 1MiB 100%
$ sudo mkfs.ext4 /dev/sdb1
```

This creates a GPT partition table on `/dev/sdb`, makes a primary partition from 1 MiB to the end of the disk, and formats the partition with the ext4 filesystem.

### 10. **Free Space Information (print free)**

The `print free` command shows not only the current partitions but also the available free space on the disk. This is useful for finding gaps where new partitions can be created.

```bash
(parted) print free
```

---

## **Partitioning a New Disk: Step-by-Step Example**

Let’s assume you have a brand new 500 GB disk at `/dev/sdb`, and you want to set it up with a GPT partition table and create two partitions:

1. A 100 GB partition for the root filesystem (`ext4`).
2. A 400 GB partition for `/home` (`ext4`).

### Step 1: Create a GPT Partition Table

```bash
$ sudo parted /dev/sdb mklabel gpt
```

This initializes a GPT partition table.

### Step 2: Create the First Partition (Root Partition)

```bash
$ sudo parted /dev/sdb mkpart primary ext4 1MiB 100GB
```

This creates a partition from 1 MiB to 100 GB.

### Step 3: Create the Second Partition (Home Partition)

```bash
$ sudo parted /dev/sdb mkpart primary ext4 100GB 500GB
```

This creates a second partition from 100 GB to the end of the disk (500 GB).

### Step 4: Format the Partitions

Now that the partitions are created, you need to format them:

```bash
$ sudo mkfs.ext4 /dev/sdb1
$ sudo mkfs.ext4 /dev/sdb2
```

This formats both partitions with the ext4 filesystem.

### Step 5: Mount the Partitions

Finally, mount the partitions:

```bash
$ sudo mount /dev/sdb1 /mnt/root
$ sudo mount /dev/sdb2 /mnt/home
```

Now you have a partitioned and formatted disk ready for use.

---

## **Summary**

`parted` is a versatile and modern disk partitioning tool that allows you to manage partitions using both MBR and GPT partition tables. It provides many features, including creating, resizing, and deleting partitions, managing alignment, and setting partition flags. Its ability to handle disks larger than 2 TB and support modern partition tables like GPT makes it a powerful tool for system administrators and users who need to manage disks effectively.

