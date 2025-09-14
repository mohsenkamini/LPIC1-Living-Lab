# Week 1 – Exploring Firmware, Hardware, and Devices

## Theme
Before deploying any services, you must understand how the system interacts with its hardware — how the kernel detects hardware, loads drivers, and exposes devices to the system.  

Your task is to perform a series of controlled experiments to explore these layers.

---

## Learning Objectives
- Understand device detection and naming in Linux
- Explore the `/dev`, `/proc`, and `/sys` interfaces
- Use `udevadm` to inspect hardware
- Learn about kernel modules and blacklisting
- Understand processes and the `/proc` filesystem

---

## Tasks

### 0. Watch Related Course Videos
- Videos 3-6 of [this playlist](https://www.youtube.com/watch?v=cqfrsmg4BKo&list=PL-tKrPVkKKE0kM18Sg5fqaZW1V2nidAeU) 


### 1. Add and Inspect Two Different Virtual Disks
- Add **two new empty virtual disks** with minimum size to your Ubuntu Server VM:  
  - One using **NVMe** Controller   
  - One using **SCSI/SATA**   
- Reboot and gather this info for **each** disk:
  - The device name (`lsblk`)
  - what driver(kernel module) is used for interacting with it
  - Its path in `/sys/block`
  - Its ID and path under `/dev/` and `/sys/`
- understand how they got different names

---

### 2. Attach and Inspect a USB Flash Drive
- Connect a USB flash drive to the Ubuntu VM.
- Confirm it appears (check `lsblk` or `dmesg | tail`).
- Explore its contents and make sure you can see it in the VM.
- Use `udevadm` to inspect it:
  - `udevadm info ...`
- Report at least the following properties:
  - The Flash USB's vendor
  - Its device type
- Repeatedly disconnect and reconnect the flash, and:
  - Using `udevadm` monitor what happens when you connect and disconnect the device
> You should be able to see relevant output on the screen when the device's connection status changes
  - Report the key events that appear on connection and disconnection


---

### 3. Blacklist the USB Storage Driver
- Find which module handles your USB flash:
- Blacklist the kernel module by adding a config file and anything else is needed.
- verify that `lsmod` shows nothing and confirms that the module is not loaded.
- Plugging the USB no longer creates the device file in `lsblk` and also you cannot see its content.
- Then **remove the blacklist** to restore functionality and confirm it works again.
- Document the before/after evidence.

---

### 4. Explore `/proc` for PID 1 and, Custom Daemon, and a process that has opened a port(like port 80 for http)
- Explore the system’s first process (PID 1) and only using info under /proc/1/ record:
  - The command it is running
  - Its status (state, threads, UID/GID)
  - One open file descriptor and explain what it is
  - One environment variable

- Next, create your own **simple daemon**:
  - Start a background process like `sleep 1000`
  - Find its PID
  - Inspect the same fields as PID 1 in `/proc/<pid>/`:
  - Compare the two processes (PID 1 vs your daemon).

- next, find a process on your system that has opened a port:
  - find out the port and the IP the process is listening on, using the contents under `/proc/<pid>`. 
---

## Deliverables
- A report file at:  
`/home/youruser/training/week1-report.txt`  

---

## Hints & Resources
- `man lsblk`, `man udevadm`, `man lsmod`
- `/sys/block/`, `/proc/`, `/dev/`
- [LPIC-1 Objectives](https://www.lpi.org/our-certifications/lpic-1-overview)
- Videos 3-6 of [this playlist](https://www.youtube.com/watch?v=cqfrsmg4BKo&list=PL-tKrPVkKKE0kM18Sg5fqaZW1V2nidAeU) 
