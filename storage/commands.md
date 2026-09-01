# Linux Storage Management

This lab demonstrates basic Linux storage management, including disk inspection, filesystem usage, file size analysis, storage allocation, and cleanup.

---

## 1. Check Filesystem Usage

### Command

```bash
df -h
```
### Purpose

Displays filesystem disk usage in a human-readable format.
### Key Information

- Total filesystem size
- Used space
- Available space
- Usage percentage
- Mount point
### Example
```bash
/dev/sdd   1007G   2.0G   954G   1%   /
```
## 2. Check Block Device
### Command
```bash
lsblk
```
### Purpose
Displays available block devices such as disks, partitions, and swap devices.
### Example 
```bash
NAME   SIZE  TYPE  FSTYPE  MOUNTPOINTS
sda    356.9M disk  ext4
sdb    159.4M disk  ext4
sdc    2G    disk  swap   [SWAP]
sdd    1T    disk  ext4   /
```
## 3. Detailed Block Device Information
### Command
```bash
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINTS
```
### Purpose

Displays detailed information about storage devices, including:

- Device name
- Size
- Device type
- Filesystem type
- Mount point

## 4. Check Directory Disk Usage
### Command
```bash
du -sh /srv/linux-admin-lab
```
### Purpose

Shows the total disk space used by a specific directory.

### Initial Result
```bash
8.0K    /srv/linux-admin-lab
```
### 5. Create a Storage Test File
## Command
```bash
sudo fallocate -l 100M /srv/linux-admin-lab/storage-test.img
```
### Purpose

Creates a 100 MB file by allocating disk space.

### Breakdown
```bash
sudo       → Run with administrator privileges
fallocate  → Allocate disk space for a file
-l 100M    → Allocate 100 MB
storage-test.img → Test file
```
## 6. Check File Size
### Command
```bash
ls -lh /srv/linux-admin-lab/storage-test.img
```
### Purpose

Displays the size of the individual file in human-readable format.

## 7. Verify Increased Directory Usage
## Command
```bash
du -sh /srv/linux-admin-lab
Result
101M    /srv/linux-admin-lab
```
The directory usage increased after creating the 100 MB test file.

## 8. Remove the Test File
## Command
```bash
sudo rm /srv/linux-admin-lab/storage-test.img
```
### Purpose

Removes the temporary storage test file and releases its allocated space.

## 9. Verify Storage Cleanup
### Command
```bash
du -sh /srv/linux-admin-lab
```
## Result
```bash
8.0K    /srv/linux-admin-lab
```
The test file was successfully removed and the directory returned to its previous size.

### Key Concepts
## Disk & Storage Commands

| Command | Purpose |
|---|---|
| `df -h` | Filesystem usage |
| `lsblk` | Disk and block device information |
| `du -sh` | Directory disk usage |
| `ls -lh` | Individual file size |
| `fallocate` | Allocate disk space |
| `rm` | Remove files |
### Lab Result

Successfully inspected Linux storage, identified block devices and filesystems, measured directory usage, allocated 100 MB of test storage, verified the increased disk usage, and cleaned up the test file.

### Skills Demonstrated

Linux Storage Management | Disk Usage Analysis | Filesystem Inspection | Block Device Inspection | File Size Analysis | Disk Space Allocation | Storage Cleanup | df | du | lsblk | fallocate | rm
