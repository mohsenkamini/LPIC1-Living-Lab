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
- Episodes 11–14 of the [playlist](https://www.youtube.com/watch?v=cqfrsmg4BKo&list=PL-tKrPVkKKE0kM18Sg5fqaZW1V2nidAeU)

---

### 2. Creating a Loop Device and Partitioning It
- **Objective**: Understand what loop devices are and how they can be used to simulate disks.
- **Task**: Create a loop device, partition it, format it with `ext4`, and write some data to the partition.
  - Create an empty file (e.g., 100MB) to simulate a disk:
    ```bash
    dd if=/dev/zero of=/tmp/testdisk.img bs=1M count=100
    ```
  - Set up the loop device:
    ```bash
    losetup /dev/loop0 /tmp/testdisk.img
    ```
  - Partition the loop device using `fdisk` and create a partition:
    ```bash
    fdisk /dev/loop0
    ```
    - Type `n` to create a new partition and use default values.
    - Type `w` to write the partition table.
  - Format the partition:
    ```bash
    mkfs.ext4 /dev/loop0p1
    ```
  - Mount the partition and write some data:
    ```bash
    mkdir /mnt/test
    mount /dev/loop0p1 /mnt/test
    echo "This is some test data" > /mnt/test/data.txt
    ```
  
---

### 3. Simulating a Partition Deletion and Recovery with `testdisk`
- **Objective**: Learn how to recover partitions after accidental deletion.
- **Task**: Simulate a mistake by deleting the partition and recover it using `testdisk`.
  - List the partitions:
    ```bash
    lsblk /dev/loop0
    ```
  - Delete the partition using `fdisk`:
    ```bash
    fdisk /dev/loop0
    ```
    - Type `d` to delete the partition.
    - Type `w` to write the changes.
  - Verify the partition is deleted by running:
    ```bash
    lsblk /dev/loop0
    ```
  - Install `testdisk`:
    ```bash
    sudo apt-get install testdisk
    ```
  - Run `testdisk` to recover the partition:
    ```bash
    sudo testdisk /dev/loop0
    ```
    - Choose "Create" to start a new log.
    - Select the disk `/dev/loop0` and "Analyse" to scan for lost partitions.
    - Write the partition table once the partition is found.
  - Verify the partition is restored and mount it again:
    ```bash
    mount /dev/loop0p1 /mnt/test
    cat /mnt/test/data.txt
    ```

---

### 4. RAID Configuration with Two Loop Devices (RAID 1 – Mirroring)
- **Objective**: Learn how to configure RAID 1 (mirroring) using loop devices.
- **Task**: Set up a RAID 1 (mirroring) array using two loop devices.
  - Create two loop devices with identical size:
    ```bash
    dd if=/dev/zero of=/tmp/loop1.img bs=1M count=100
    dd if=/dev/zero of=/tmp/loop2.img bs=1M count=100
    losetup /dev/loop1 /tmp/loop1.img
    losetup /dev/loop2 /tmp/loop2.img
    ```
  - Create a RAID 1 array using `mdadm`:
    ```bash
    sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/loop1 /dev/loop2
    ```
  - Format the RAID device:
    ```bash
    mkfs.ext4 /dev/md0
    ```
  - Mount the RAID device and write some data:
    ```bash
    mkdir /mnt/raid
    mount /dev/md0 /mnt/raid
    echo "RAID 1 test data" > /mnt/raid/test.txt
    ```
  - Verify the data is on both devices:
    - Check `/dev/loop1` and `/dev/loop2` using `lsblk`.

---

### 5. Partition Backup and Recovery using `dd` and `testdisk`
- **Objective**: Understand how to back up and recover partitions.
- **Task**: Backup a partition using `dd` and restore it to another loop device.
  - Create a new loop device to restore the partition:
    ```bash
    dd if=/dev/zero of=/tmp/testdisk_restore.img bs=1M count=100
    losetup /dev/loop3 /tmp/testdisk_restore.img
    ```
  - Partition the new loop device and format it:
    ```bash
    fdisk /dev/loop3
    mkfs.ext4 /dev/loop3p1
    ```
  - Backup the partition from `/dev/loop0p1` to the backup file:
    ```bash
    dd if=/dev/loop0p1 of=/tmp/backup.img
    ```
  - Restore the backup to the new loop device:
    ```bash
    dd if=/tmp/backup.img of=/dev/loop3p1
    ```
  - Mount the restored partition and verify data:
    ```bash
    mount /dev/loop3p1 /mnt/restored
    cat /mnt/restored/data.txt
    ```

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


