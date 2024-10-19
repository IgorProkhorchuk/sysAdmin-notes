Here are several practical tasks related to inodes, along with explanations and solutions, to help you understand and apply the concepts. These tasks will involve file creation, hard links, inode inspection, inode limit testing, and more.

---

### Task 1: Inspect Inode Numbers for Files

**Objective**: Display the inode numbers for several files in a directory.

#### Steps:
1. Create two files: `file1.txt` and `file2.txt`.
2. Use the `ls` command to view the inode numbers for these files.

#### Commands:

```bash
$ touch file1.txt file2.txt           # Create two empty files
$ ls -li                              # List files with inode numbers
```

#### Expected Output:

```
128483 -rw-r--r-- 1 user user 0 Oct 19 12:30 file1.txt
128484 -rw-r--r-- 1 user user 0 Oct 19 12:30 file2.txt
```

#### Explanation:
- The `-i` option in `ls` displays the inode numbers of the files.
- Each file has a unique inode number (e.g., `128483` for `file1.txt` and `128484` for `file2.txt`).

---

### Task 2: Create a Hard Link and Verify the Inode

**Objective**: Create a hard link and verify that both the original file and the hard link share the same inode.

#### Steps:
1. Create a file named `file1.txt`.
2. Create a hard link named `file1_hard.txt` to `file1.txt`.
3. Use `ls -li` to display the inode numbers of both files.

#### Commands:

```bash
$ echo "Hello World" > file1.txt        # Create file1.txt with content
$ ln file1.txt file1_hard.txt           # Create a hard link
$ ls -li                                # Display inode numbers
```

#### Expected Output:

```
128483 -rw-r--r-- 2 user user 12 Oct 19 12:45 file1.txt
128483 -rw-r--r-- 2 user user 12 Oct 19 12:45 file1_hard.txt
```

#### Explanation:
- Both `file1.txt` and `file1_hard.txt` share the same inode number (`128483`), meaning they reference the same file data.
- The link count (`2`) shows that two directory entries (one for `file1.txt` and one for `file1_hard.txt`) are pointing to the same inode.

---

### Task 3: Create a Symbolic Link and Compare with a Hard Link

**Objective**: Create a symbolic link and a hard link, then compare the inode numbers.

#### Steps:
1. Create a file named `file1.txt`.
2. Create a symbolic link named `file1_sym.txt` and a hard link named `file1_hard.txt`.
3. Use `ls -li` to compare the inode numbers of the three files.

#### Commands:

```bash
$ echo "Hello World" > file1.txt         # Create file1.txt with content
$ ln file1.txt file1_hard.txt            # Create a hard link
$ ln -s file1.txt file1_sym.txt          # Create a symbolic link
$ ls -li                                 # Display inode numbers
```

#### Expected Output:

```
128483 -rw-r--r-- 2 user user 12 Oct 19 12:50 file1.txt
128483 -rw-r--r-- 2 user user 12 Oct 19 12:50 file1_hard.txt
128485 lrwxrwxrwx 1 user user  9 Oct 19 12:50 file1_sym.txt -> file1.txt
```

#### Explanation:
- The inode number for `file1.txt` and `file1_hard.txt` is the same (`128483`), indicating they share the same inode.
- The symbolic link `file1_sym.txt` has a different inode number (`128485`), as it is a separate file containing a reference (a path) to `file1.txt`.

---

### Task 4: Test Inode Limit

**Objective**: Simulate a scenario where you run out of inodes by creating many small files, even though disk space is still available.

#### Steps:
1. Create a directory called `test_inodes`.
2. Use a loop to create many small files within this directory.
3. Check the inode usage with `df -i`.

#### Commands:

```bash
$ mkdir test_inodes                      # Create a test directory
$ cd test_inodes
$ for i in {1..1000000}; do touch file_$i; done  # Create 1 million small files
$ df -i                                   # Check inode usage
```

#### Expected Output (after some time):

```
Filesystem      Inodes    IUsed    IFree IUse% Mounted on
/dev/sda1      1280000  1280000        0  100% /
```

#### Explanation:
- After running the loop, the inode usage reaches 100%, meaning no new files can be created even if there is available disk space.
- You have exhausted all available inodes, and you will receive errors if you try to create more files.

---

### Task 5: Use `stat` to Inspect File Metadata

**Objective**: Use the `stat` command to display detailed inode and metadata information for a file.

#### Steps:
1. Create a file named `file1.txt`.
2. Use the `stat` command to inspect the inode number, file size, and other metadata.

#### Commands:

```bash
$ echo "Hello World" > file1.txt        # Create file1.txt with content
$ stat file1.txt                        # Display detailed file information
```

#### Expected Output:

```
  File: file1.txt
  Size: 12          Blocks: 8          IO Block: 4096   regular file
Device: 801h/2049d  Inode: 128483       Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/   user)   Gid: ( 1000/   user)
Access: 2024-10-19 12:55:34.000000000 +0200
Modify: 2024-10-19 12:55:34.000000000 +0200
Change: 2024-10-19 12:55:34.000000000 +0200
 Birth: -
```

#### Explanation:
- **Inode**: The inode number of the file is `128483`.
- **Links**: The file has 1 hard link (meaning only `file1.txt` points to this inode).
- **Access/Modify/Change**: The timestamps show when the file was last accessed, modified, and when the metadata was last changed.

---

### Task 6: Create a Large File and Examine Indirect Pointers

**Objective**: Create a large file that exceeds the inode's direct block pointers and uses indirect pointers.

#### Steps:
1. Create a large file (e.g., 1 GB) using `dd`.
2. Use the `stat` command to inspect the file size and block allocation.

#### Commands:

```bash
$ dd if=/dev/zero of=largefile bs=1M count=1024  # Create a 1 GB file
$ stat largefile                                # Display file information
```

#### Expected Output:

```
  File: largefile
  Size: 1073741824     Blocks: 2097152    IO Block: 4096   regular file
Device: 801h/2049d  Inode: 128487       Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/   user)   Gid: ( 1000/   user)
Access: 2024-10-19 12:58:12.000000000 +0200
Modify: 2024-10-19 12:58:12.000000000 +0200
Change: 2024-10-19 12:58:12.000000000 +0200
 Birth: -
```

#### Explanation:
- The large file's size (1 GB) exceeds what can be managed by direct pointers in the inode. The file system uses indirect pointers to manage this large file.
- The `Blocks` field shows the number of 512-byte blocks allocated to the file (e.g., `2097152` blocks for 1 GB).

---

### Task 7: Simulate File Deletion and Inode Reuse

**Objective**: Delete a file, then create a new file to observe inode reuse.

#### Steps:
1. Create a file named `file1.txt`.
2. Delete the file and immediately create a new file with a different name.
3. Compare the inode numbers of both files.

#### Commands:

```bash
$ echo "File 1" > file1.txt             # Create file1.txt
$ ls -i file1.txt                       # Check its inode number
$ rm file1.txt                          # Delete the file
$ echo "File 2" > file2.txt             # Create a new file
$ ls -i file2.txt                       # Check the inode number
```

#### Expected Output:

```
128483 file1.txt      # Before deletion
128483 file2.txt      # After deletion and recreation
```

#### Explanation:
- After deleting `file1.txt`, the inode (`128483`) is freed and can be reused by the file system.
- When `file2.txt

` is created, it might reuse the same inode, demonstrating inode recycling.

---
