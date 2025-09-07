# Week 0 – Lab Setup and Orientation

## Theme
Imagine you are joining the infrastructure team for a small company that wants to run its services on Linux but it's currently not.  
Before you can start working on bringing the services up, you need to prepare your environment.  

> This environment will be used throughout the whole training, so treat it like your own production system.

---

## Learning Objectives
- Understand the lab environment structure  
- Setup two different Linux distributions  
- Connect to your machines via SSH  
- Get comfortable with the terminal to discover basic info on your machines  
- Verify that your system is ready for the upcoming weeks  

---

## Lab Environment
Your lab consists of two machines that you will build and use throughout the training.  

| Machine      | OS                   | Role                   | Hostname   | CPU | RAM  | Disk   | IP Address     |
|--------------|----------------------|------------------------|------------|-----|------|--------|----------------|
| Jump Host    | Fedora (latest stable) | Gateway & admin node  | `jump`     | 1 vCPU | 1 GB | 10 GB | 192.168.56.10 |
| Prod Server  | Ubuntu LTS (latest)    | Main application server | `server1` | 1 vCPU | 2 GB | 20 GB | 192.168.56.11 |

> Later in the course, new servers may be added to simulate a more realistic environment.  

**Networking requirements:**
- Both machines must be on the **same internal network** in your hypervisor (VirtualBox, VMware, KVM, etc.).  
- Choose a private subnet (e.g., `192.168.56.0/24`) that does not conflict with your home or office LAN.  

---

## Tasks

1. **Create the Virtual Machines** using your hypervisor and install OS on the machines 
   - Use the table above as reference for configuring CPU, RAM, disk, hostname, and IP addresses.  
   - Make sure both machines are connected to the same internal network.  

2. **Configure & Check Networking Status**  
   - Assign the IP addresses as shown in the table.  
   - Verify connectivity between the two machines using `ping`.  
   - Ensure you can SSH from your host machine → Jump Host → Prod Server.  

3. **Set & Verify Hostnames**  
   - On Fedora (Jump Host), set the hostname to `jump`.  
   - On Ubuntu (Prod Server), set the hostname to `server1`.  
   - Verify with:  
     ```bash
     hostnamectl
     ```  

4. **Explore the system**  
   - Verify which distribution and version you’re using (`cat /etc/os-release`).  
   - Check kernel version with `uname -r`.  
   - Display system uptime with `uptime`.  

5. **Basic navigation**  
   - Practice moving around the filesystem (`cd`, `ls`, `pwd`).  
   - Create a personal working directory under `/home/youruser/training`.  

6. **Watch Related Course Videos**
   - The first three videos of [this playlist](https://www.youtube.com/watch?v=cqfrsmg4BKo&list=PL-tKrPVkKKE0kM18Sg5fqaZW1V2nidAeU)

6. **First report**  
   - Create a text file `/home/youruser/training/week0-report.txt` with the following info:  
     - Your username  
     - Hostname  
     - OS name and version  
     - Kernel version  
     - System uptime at the time of login  
   - Use `nano`, `vim`, or `echo` with redirection to create the file.  

---

## Deliverable
- A file at: `/home/youruser/training/week0-report.txt`
- Contents should match the system info you discovered.  

---

## Hints & Resources
- `man uname`  
- `man uptime`  
- `man hostnamectl`  
- LPIC-1 official objectives: [Linux Professional Institute LPIC-1](https://www.lpi.org/our-certifications/lpic-1-overview)  
- The first three videos of [this playlist](https://www.youtube.com/watch?v=cqfrsmg4BKo&list=PL-tKrPVkKKE0kM18Sg5fqaZW1V2nidAeU)


