# Week 0 – Lab Setup and Orientation

## Theme
Imagine you are joining the infrastructure team for a small company that wants to run its services on Linux but it's currently not.  
Before you can start working on bringing the services up, you need to prepare your environment.  

> This environment will be used throughout the whole training, so treat it like your own production system.

---

## Learning Objectives
- Understand the lab environment structure  
- Setup two different Linux distribuitions
- Connect to your machines via SSH  
- Get comfortable with the terminal to discover basic info on your machines
- Verify that your system is ready for the upcoming weeks

---

## Lab Environment
Your lab consists of:
- **Jump Host** – a gateway you'll use to access other servers
- **Prod Server (server1)** – the main system where you’ll perform tasks  

Later in the course, new servers will be added.

## Lab Environment
Your lab consists of two machines that you will build and use throughout the training.  

| Machine      | OS            | Role        | CPU | RAM  | Disk   |
|--------------|---------------|-------------|-----|------|--------|
| Jump Host    | Fedora (latest stable) | Gateway & admin node | 1 vCPU | 1 GB | 10 GB |
| Prod Server  | Ubuntu LTS (latest)    | Main application server | 1 vCPU | 2 GB | 20 GB |

> Later in the course, new servers may be added to simulate a more realistic environment.  


---

## Tasks

1. **Connect to your lab**
   - Use the credentials provided by your supervisor to SSH into the jump host:
     ```bash
     ssh youruser@jump.example.com
     ```
   - From the jump host, connect to `server1`:
     ```bash
     ssh youruser@server1
     ```

2. **Explore the system**
   - Find out which distribution and version you’re using (`cat /etc/os-release`).  
   - Check kernel version with `uname -r`.  
   - Display system uptime with `uptime`.  

3. **Basic navigation**
   - Practice moving around the filesystem (`cd`, `ls`, `pwd`).  
   - Create a personal working directory under `/home/youruser/training`.  

4. **First report**
   - Create a text file `/home/youruser/training/week0-report.txt` with the following info:
     - Your username
     - OS name and version
     - Kernel version
     - System uptime at the time of login
   - Use `nano`, `vim`, or `echo` with redirection to create the file.  

---

## Deliverable
- A file at:  
    `/home/youruser/training/week0-report.txt`
    Contents should match the system info you discovered.  

---

## Hints & Resources
- `man uname`  
- `man uptime`  
- LPIC-1 official objectives: [Linux Professional Institute LPIC-1](https://www.lpi.org/our-certifications/lpic-1-overview)  

