Let’s do some practical tasks using RAID 0 and RAID 1.


Here are some example tasks:

---

### **Preparation for Both RAID 0 and RAID 1**:
Before proceeding with the specific tasks, ensure that you have at least two (for RAID 1) or three (for RAID 0) virtual hard drives added to your Debian VM in VirtualBox. Here’s how you can add virtual disks:

1. **Add Virtual Disks**:
   - Open **VirtualBox**.
   - Select your Debian VM and go to **Settings** > **Storage**.
   - Click the **Controller: SATA** and add new **hard disks** by clicking the "+" button.
   - Set the disk size (e.g., 2GB each for practice) and repeat until you have at least two additional disks.

2. **Install `mdadm` (RAID management tool)**:
   - Boot into your Debian VM and install `mdadm`, the RAID management software.
     ```bash
     sudo apt update
     sudo apt install mdadm
     ```

---

### **Task 1: Set Up RAID 0 (Striping)**

#### 1.1. **Create a RAID 0 Array**
Objective: Combine multiple drives into a RAID 0 array to maximize performance.
  
1. **List your new disks** to ensure they are available:
   ```bash
   lsblk
   ```
   You should see new devices like `/dev/sdb`, `/dev/sdc`, etc.

2. **Create the RAID 0 array** using `mdadm`. Assuming `/dev/sdb` and `/dev/sdc` are your new disks:
   ```bash
   sudo mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/sdb /dev/sdc
   ```

3. **Verify the RAID 0 array**:
   ```bash
   cat /proc/mdstat
   ```
   You should see something like `md0` with RAID level 0.

4. **Format the RAID array**:
   ```bash
   sudo mkfs.ext4 /dev/md0
   ```

5. **Mount the RAID array**:
   - Create a mount point:
     ```bash
     sudo mkdir /mnt/raid0
     ```
   - Mount the RAID array:
     ```bash
     sudo mount /dev/md0 /mnt/raid0
     ```

6. **Verify that it's mounted** by checking the available disk space:
   ```bash
   df -h
   ```

#### 1.2. **Task**: Write and Read Test
- Write a file to your RAID 0 array and verify the performance:
   ```bash
   sudo dd if=/dev/zero of=/mnt/raid0/testfile bs=1M count=1000
   ```
- Measure the write and read speed using `hdparm` (install if necessary).
   ```bash
   sudo apt install hdparm
   sudo hdparm -t /dev/md0
   ```

#### 1.3. **Task**: Remove RAID 0
- Unmount and stop the RAID array when you’re done:
   ```bash
   sudo umount /mnt/raid0
   sudo mdadm --stop /dev/md0
   sudo mdadm --remove /dev/md0
   ```

---

### **Task 2: Set Up RAID 1 (Mirroring)**

#### 2.1. **Create a RAID 1 Array**
Objective: Set up RAID 1 to mirror data across two disks for redundancy.

1. **Create the RAID 1 array** with two disks:
   ```bash
   sudo mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/sdb /dev/sdc
   ```

2. **Verify the RAID 1 array**:
   ```bash
   cat /proc/mdstat
   ```
   This should show `md1` with RAID level 1.

3. **Format and mount the RAID array**:
   - Format:
     ```bash
     sudo mkfs.ext4 /dev/md1
     ```
   - Mount the RAID 1 array:
     ```bash
     sudo mkdir /mnt/raid1
     sudo mount /dev/md1 /mnt/raid1
     ```

4. **Verify the mounted RAID array**:
   ```bash
   df -h
   ```

#### 2.2. **Task**: Simulate a Disk Failure
Objective: Simulate a disk failure to see RAID 1’s redundancy in action.

1. **Remove one of the disks** from the array:
   ```bash
   sudo mdadm /dev/md1 --fail /dev/sdb --remove /dev/sdb
   ```

2. **Check the RAID status**:
   ```bash
   cat /proc/mdstat
   ```
   You’ll see that `md1` is degraded, but still operational.

3. **Re-add the disk (simulate disk replacement)**:
   ```bash
   sudo mdadm /dev/md1 --add /dev/sdb
   ```

4. **Monitor the rebuilding process**:
   ```bash
   watch cat /proc/mdstat
   ```

#### 2.3. **Task**: Auto-Assembly on Boot
Ensure that your RAID array is auto-assembled on boot:

1. **Update `mdadm` configuration**:
   ```bash
   sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
   ```

2. **Update the initramfs**:
   ```bash
   sudo update-initramfs -u
   ```

---

#Apologies for not finishing the task earlier! Let's continue with the steps to set up RAID monitoring and management.

### **Optional Task 3: RAID Monitoring and Management**

#### 3.1. **Configure Email Notifications for RAID Events**
Objective: Set up email alerts to notify you in case of RAID issues, such as a disk failure.

1. **Configure `mdadm` to send email alerts**:
   Run the following command to configure `mdadm` for monitoring and set an email address for notifications.
   ```bash
   sudo dpkg-reconfigure mdadm
   ```
   - During this process, you'll be prompted to enter the email address where notifications should be sent.
   - Accept the default options for other settings unless you have specific requirements.

2. **Edit the `mdadm.conf` file to ensure proper monitoring configuration**:
   Open the configuration file:
   ```bash
   sudo nano /etc/mdadm/mdadm.conf
   ```
   - Ensure that the `MAILADDR` line is set to your desired email address:
     ```bash
     MAILADDR your_email@example.com
     ```

3. **Restart the `mdadm` service** to apply the changes:
   ```bash
   sudo systemctl restart mdadm
   ```

#### 3.2. **Enable Monitoring Daemon**
The monitoring daemon will run in the background and notify you of any RAID issues.

1. **Start and enable the `mdadm` monitoring service**:
   ```bash
   sudo systemctl enable --now mdadm
   ```

2. **Check the status of the monitoring service**:
   You can verify that the monitoring daemon is running properly:
   ```bash
   sudo systemctl status mdadm
   ```

   This should show the service as active.

#### 3.3. **Test RAID Monitoring (Optional)**
You can simulate a failure to test if you receive an email notification. You’ve done this before in **Task 2.2**, where you failed and removed a disk from the RAID 1 array:

```bash
sudo mdadm /dev/md1 --fail /dev/sdb --remove /dev/sdb
```

- After this, check your email to confirm that the notification was sent.
- Re-add the disk to simulate the disk replacement and confirm the rebuild process.

---

### **Bonus Task: Log Monitoring**
You can monitor RAID events through system logs, which is another way to keep track of any RAID-related issues.

1. **Use `journalctl` to monitor RAID logs**:
   ```bash
   sudo journalctl -u mdadm
   ```

2. **Check `/var/log/syslog` for RAID events**:
   RAID-related messages are also logged to `/var/log/syslog`. You can filter for `mdadm` events like this:
   ```bash
   grep mdadm /var/log/syslog
   ```

---

Now you have RAID 0 and RAID 1 setup and monitoring configured, including email notifications for RAID events. This setup will help you manage and monitor your RAID arrays efficiently.