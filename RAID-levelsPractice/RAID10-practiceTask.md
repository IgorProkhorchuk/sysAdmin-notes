RAID 10 (also called RAID 1+0) is a combination of RAID 1 (mirroring) and RAID 0 (striping). It provides the redundancy of RAID 1 with the performance benefits of RAID 0, offering both data protection and fast data access. RAID 10 requires at least **four disks**.

Here are some example tasks for RAID 10 using VirtualBox and Debian 12:

---

### **Task 1: Set Up a RAID 10 Array**

#### 1.1. **Create a RAID 10 Array**
Objective: Combine four or more disks into a RAID 10 array, providing redundancy and performance.

1. **Prepare your virtual environment** by adding at least **four virtual hard drives** in VirtualBox (similar to the setup for RAID 5 and RAID 6).

2. **List your new disks**:
   After booting into Debian, verify the new drives are recognized:
   ```bash
   lsblk
   ```
   You should see `/dev/sdb`, `/dev/sdc`, `/dev/sdd`, and `/dev/sde`.

3. **Create the RAID 10 array** using `mdadm`:
   ```bash
   sudo mdadm --create /dev/md10 --level=10 --raid-devices=4 /dev/sdb /dev/sdc /dev/sdd /dev/sde
   ```

   - `--level=10` specifies RAID 10.
   - Replace `/dev/sdb`, `/dev/sdc`, etc., with the actual names of your disks.

4. **Monitor the RAID creation process**:
   Use the following command to check the status of RAID 10 creation:
   ```bash
   cat /proc/mdstat
   ```

5. **Format the RAID 10 array** with a file system (e.g., ext4):
   ```bash
   sudo mkfs.ext4 /dev/md10
   ```

6. **Mount the RAID array**:
   - Create a mount point:
     ```bash
     sudo mkdir /mnt/raid10
     ```
   - Mount the array:
     ```bash
     sudo mount /dev/md10 /mnt/raid10
     ```

7. **Verify the mount**:
   Ensure the RAID 10 array is mounted:
   ```bash
   df -h
   ```

#### 1.2. **Task**: Test Disk Performance
Objective: Compare the performance of the RAID 10 array to other RAID levels (RAID 5, RAID 6).

1. **Write a test file** to the RAID 10 array:
   ```bash
   sudo dd if=/dev/zero of=/mnt/raid10/testfile bs=1M count=1000
   ```

2. **Measure the read/write speed** of the RAID 10 array:
   ```bash
   sudo hdparm -t /dev/md10
   ```

---

### **Task 2: Simulate a Disk Failure in RAID 10**

RAID 10 can tolerate the failure of one or more disks (depending on which disks fail). Let’s simulate a failure and then recover the array.

#### 2.1. **Simulate a Disk Failure**
Objective: Remove one disk from the RAID array and observe how the array handles the failure.

1. **Fail one of the disks** (e.g., `/dev/sdb`) to simulate a disk failure:
   ```bash
   sudo mdadm /dev/md10 --fail /dev/sdb --remove /dev/sdb
   ```

2. **Check the status of the RAID array**:
   ```bash
   cat /proc/mdstat
   ```
   The array should now show that it is degraded but still operational.

3. **Test if you can still access data**:
   Try accessing files from the mounted RAID array:
   ```bash
   ls /mnt/raid10
   ```

#### 2.2. **Task**: Rebuild the Array After Disk Failure
Objective: Replace the failed disk and rebuild the RAID 10 array to restore redundancy.

1. **Add a new disk** (or re-add the same disk after "replacing" it) to the array:
   ```bash
   sudo mdadm /dev/md10 --add /dev/sdb
   ```

2. **Monitor the rebuilding process**:
   ```bash
   watch cat /proc/mdstat
   ```

   The RAID array will rebuild the missing data onto the new disk. This process can take time depending on the size of the disks.

3. **Check the RAID status** after the rebuild:
   ```bash
   sudo mdadm --detail /dev/md10
   ```

   The array should now be healthy again.

---

### **Task 3: Configure RAID 10 for Auto-Assembly on Boot**

Ensure your RAID 10 array automatically assembles and mounts on boot.

#### 3.1. **Configure Auto-Assembly**

1. **Add the RAID array to `mdadm` configuration**:
   Update the configuration so the system auto-detects the RAID array at boot:
   ```bash
   sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
   ```

2. **Update the initramfs**:
   Update the initramfs so the RAID array is recognized during boot:
   ```bash
   sudo update-initramfs -u
   ```

#### 3.2. **Automatically Mount the RAID Array**

1. **Edit the `/etc/fstab` file** to ensure the array mounts automatically:
   ```bash
   sudo nano /etc/fstab
   ```

2. **Add a new line** for the RAID array:
   ```bash
   /dev/md10  /mnt/raid10  ext4  defaults  0  0
   ```

3. **Test the `fstab` entry**:
   Unmount the array and test if it mounts correctly using `/etc/fstab`:
   ```bash
   sudo umount /mnt/raid10
   sudo mount -a
   ```

---

### **Task 4: Monitor RAID 10 Health**

It is essential to monitor the health of your RAID 10 array to catch potential issues early.

#### 4.1. **Set Up RAID Monitoring**
Objective: Configure automatic RAID monitoring with email alerts.

1. **Reconfigure `mdadm` to send email notifications** in case of disk failure or degradation:
   ```bash
   sudo dpkg-reconfigure mdadm
   ```

2. **Verify the `mdadm.conf` configuration** file has the correct email address for notifications:
   ```bash
   sudo nano /etc/mdadm/mdadm.conf
   ```
   Look for the `MAILADDR` line and ensure it has your correct email address:
   ```bash
   MAILADDR your_email@example.com
   ```

3. **Restart the `mdadm` monitoring service**:
   ```bash
   sudo systemctl restart mdadm
   ```

4. **Check RAID status manually**:
   Use `mdadm` to get a detailed report of your RAID array’s status:
   ```bash
   sudo mdadm --detail /dev/md10
   ```

#### 4.2. **Task**: Simulate Monitoring Notification
Simulate a disk failure to test if the monitoring system sends an email alert.

```bash
sudo mdadm /dev/md10 --fail /dev/sdb --remove /dev/sdb
```

- After the failure, check if the email notification is sent.
- Re-add the disk and monitor the rebuild process.

---

### **Task 5: Expand the RAID 10 Array**

RAID 10 supports the expansion of the array by adding more disks, increasing storage and performance.

#### 5.1. **Expand the Array by Adding New Disks**
Objective: Add two new disks to the RAID 10 array and grow the filesystem.

1. **Add two additional virtual disks** to your VirtualBox Debian VM (e.g., `/dev/sdf` and `/dev/sdg`).

2. **Add the new disks to the RAID array**:
   ```bash
   sudo mdadm --add /dev/md10 /dev/sdf /dev/sdg
   ```

3. **Grow the RAID array**:
   ```bash
   sudo mdadm --grow /dev/md10 --raid-devices=6
   ```

4. **Resize the filesystem** to use the new space:
   ```bash
   sudo resize2fs /dev/md10
   ```

5. **Verify the expansion**:
   Check the disk space after adding the new disks:
   ```bash
   df -h
   ```

---

### **Task 6: Benchmark RAID 10 Performance**

Objective: Compare the performance of RAID 10 with other RAID levels.

1. **Benchmark read/write performance**:
   Write a test file to the RAID 10 array and measure the performance:
   ```bash
   sudo dd if=/dev/zero of=/mnt/raid10/testfile bs=1M count=1000
   ```

2. **Measure file operation performance** and compare it with RAID 5, RAID 6, or RAID 1 from your previous tasks.

---

### **Conclusion**:
RAID 10 offers the best of both worlds, combining redundancy with performance. These tasks will give you a practical understanding of how RAID 10 operates and how it compares to other RAID levels in terms of redundancy, speed, and storage capacity.