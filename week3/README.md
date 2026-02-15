# Week 3 – Disk Management, Loop Devices, and RAID

## Theme
In this week, you'll learn about working with virtual disk devices, partitions, and data recovery. You'll create a loop device, partition it, simulate a partition failure, and recover it. Additionally, you will explore RAID configurations and partition backup and recovery, providing a solid foundation for disk management.

---

## Learning Objectives
- Create and manage loop devices
- Partition loop devices and understand partition tables
- Simulate partition deletion and recover using `testdisk`
- Set up RAID 1 (mirroring) using loop devices
- Backup and restore partitions using `dd` and `testdisk`

---

## Tasks

### 1. Watch Related Course Videos
- Episodes 37-40 of the [playlist](https://www.youtube.com/watch?v=cqfrsmg4BKo&list=PL-tKrPVkKKE0kM18Sg5fqaZW1V2nidAeU)

---

### 2. Creating a Loop Device and Partitioning It
- **Objective**: Understand what loop devices are and how they can be used to simulate disks.
- **Task**: Create a loop device, partition it, format it with `ext4`, and write some data to the partition.
  - Create an empty file (e.g., 100MB) to simulate a disk
  - Set up the loop device
  - Partition the loop device using `fdisk` and create a partition
  - Format the partition
  - Mount the partition and write some data in a file
  
---

### 3. Simulating a Partition Deletion and Recovery with `testdisk`
- **Objective**: Learn how to recover partitions after accidental deletion.
- **Task**: Simulate a mistake by deleting the partition and recover it using `testdisk`.
  - Delete the partition using `fdisk`:
    ```bash
    fdisk /dev/loop<x>
    ```
    - Type `d` to delete the partition.
    - Type `w` to write the changes.
  - Verify the partition is deleted by running:
    ```bash
    lsblk /dev/loop<x>
    ```
  - Install `testdisk`:
  - Run `testdisk` to recover the partition
  - Verify the partition is restored and mount it again
    ```bash
    mount /dev/loop0p1 /mnt/test
    cat /mnt/test/data.txt
    ```

---

### 4. RAID Configuration with Two Loop Devices (RAID 1 – Mirroring)
- **Objective**: Learn how to configure RAID 1 (mirroring) using loop devices.
- **Task**: Set up a RAID 1 (mirroring) array using two loop devices.
  - Create two loop devices with identical size:
  - Create a RAID 1 array using `mdadm`:
  - Format the RAID device:
  - Mount the RAID device and write some data in it:
    ```bash
    ....
    echo "RAID 1 test data" > /mnt/raid/test.txt
    ```
  - Verify the data is on both devices

---

### 5. Partition Backup and Recovery using `dd` and `testdisk`
- **Objective**: Understand how to back up and recover partitions.
- **Task**: Backup a partition using `dd` and restore it to another loop device.
  - Create a new loop device to restore the partition:
  - Partition the new loop device and format it:
  - Backup the partition from `/dev/loop0p1` to the backup file:
  - Restore the backup to the new loop device:
  - Mount the restored partition and verify data:

---

## Deliverables
- A report at:  
`/home/youruser/training/week3-report.txt`  

Report should include:  
- Evidence of loop device creation, partitioning, and data writing  
- Steps for partition deletion and recovery using `testdisk`  
- RAID 1 setup and data verification  
- Partition backup and recovery using `dd` and `testdisk`  
- Logs from the recovery steps with explanations

---

## Hints & Resources
- `man losetup`, `man fdisk`, `man mdadm`  
- `man testdisk` for partition recovery details  
- [RAID Levels Overview](https://www.techradar.com/news/what-is-raid)  
- [LPIC-1 Objectives](https://www.lpi.org/our-certifications/lpic-1-overview)  


