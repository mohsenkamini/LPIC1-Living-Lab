# Week 2 – Boot, Init, and Systemd

## Theme
Now that your machines are running, it’s time to understand how they start, stop, and manage services. You’ll work with `systemd`, explore runlevels/targets, experiment with GRUB, and practice debugging and recovery.  

---

## Learning Objectives
- Manage services with `systemctl`  
- Understand systemd units, dependencies, and targets  
- Compare systemd with SysV init scripts and runlevels  
- Work with GRUB and kernel boot options 
- Practice recovery from misconfiguration  

---

## Tasks

### 0. Watch Related Course Videos
- Episodes 7–10 of the [playlist](https://www.youtube.com/watch?v=cqfrsmg4BKo&list=PL-tKrPVkKKE0kM18Sg5fqaZW1V2nidAeU)  

---

### 1. Service Management & SSH Hardening
On both machines do:
- Edit `/etc/ssh/sshd_config` to disable:  
  - Root login  
- Restart sshd with `systemctl restart sshd`.  
- Test access to confirm changes.  

---

### 2. Processes, Trees, and Services
- Run a simple process (`sleep 1000`) and trace it with `pstree`. Report and understand what the parent processes are. 
- Use `ss -ntulp` to find a process that has opened a port.  
- Trace it in `pstree`, Report and understand who the parents are. Then find its systemd service, and inspect logs with:  
  - `systemctl status`  
  - `journalctl -u <service>`  
- Open the unit file of the service and briefly explain each section.  

---

### 3. Custom systemd Services
- Create a service that runs `dmesg` and puts the output logs into a file.  
- Create another service that depends on the first and prints the file as its own logs.  
- Show how the dependency prevents the second service from running unless the first has started.  

---

### 4. Runlevels and Targets
- List systemd targets and compare to SysV runlevels. 
- Switch between them (`systemctl isolate`), then set a default target.  
- Configure a target in a way that the system boots **without network**. Then you should revert the changes and confirm everything works fine.

---

### 5. GRUB and Recovery
- On Fedora, without entering the current password of the root user, reset the root's password by editing GRUB. (This is called root recovery process. Think of it like you have lost your password. What would you do?)

---

### 6. Shutdown and Reboot
- From now on, always shut down and reboot using CLI commands! :_) 

---

## Deliverables
- A report at:  
`/home/youruser/training/week2-report.txt`  

Report should include:  
- Evidence of SSH configuration and result of it  
- Process tree examples and systemd service mapping  
- Logs from the custom services and explanation of dependency  
- Proof of runlevel/target switching and recovery  
- GRUB experiments and root password reset  
- CLI shutdown/reboot usage  

---

## Hints & Resources
- `man systemctl`, `man journalctl`, `man sshd_config`  
- `/etc/systemd/system/` for custom units  
- `man grub2`  
- [LPIC-1 Objectives](https://www.lpi.org/our-certifications/lpic-1-overview)  

