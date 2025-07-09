# 🚀 Deploying and Managing a Departmental Web Server on RHEL 9

👨‍💻 **Role**: Junior System Administrator  
🏢 **Company**: DevCore Solutions  
📦 **Environment**: Red Hat Enterprise Linux 9

---

## 🧾 Introduction

As a junior system administrator at **DevCore Solutions**, I have been tasked with designing, deploying, and managing a secure internal web server environment using **Red Hat Enterprise Linux 9 (RHEL 9)**. This project simulates real-world sysadmin responsibilities by walking through critical phases such as system setup, user and group management, web server configuration, security enforcement with SELinux, task automation, log handling, and network configuration.

Each phase of this project is designed to reflect foundational objectives from the **RH124 course**, helping reinforce core Linux administration skills through practical application. All tasks have been executed in a structured, documented, and security-conscious manner to simulate production-like standards.

The goal is to ensure that the development team has a stable, secure, and functional internal web platform while maintaining best practices in Linux system administration.


---

## 📌 Phase 1: Initial Setup and User Management

🗓️ **Context**:  
Onboarding as a new sysadmin, I started by setting up the system and creating accounts for our development team.

🔸 I installed RHEL 9 and configured the hostname, timezone, and installed all system updates.  
🔸 I created three user accounts: `devalpha`, `devbeta`, and `devadmin`.  
🔸 I created a new group called `developers` and added all three users to it.  
🔸 I granted `devadmin` passwordless sudo privileges using a rule in `/etc/sudoers.d/devadmin`.

📸 **Deliverables**:
- Screenshot of `/etc/passwd`
- Output of `id devalpha`
- Output of `sudo -l -U devadmin`

---

## 📌 Phase 2: Directory and Permission Configuration

🗓️ **Context**:  
With users ready, I prepared a structured directory for the development web environment.

🔸 I created the directory `/opt/devweb` with subdirectories: `config`, `logs`, `scripts`, and `html`.  
🔸 I assigned group ownership of the entire `/opt/devweb` structure to the `developers` group.  
🔸 I set the SGID (Set Group ID) bit on `/opt/devweb/scripts` so that new files inherit group ownership.

📸 **Deliverables**:
- Output of `ls -lR /opt/devweb`
- Commands used for `chmod` and `chgrp`

---

## 📌 Phase 3: Apache Installation and Configuration

🗓️ **Context**:  
I deployed Apache to host the development website internally.

🔸 I installed the Apache web server using `dnf install -y httpd`.  
🔸 I enabled and started the Apache service with `systemctl enable --now httpd`.  
🔸 I created a simple `index.html` file inside `/opt/devweb/html`.  
🔸 I updated the `DocumentRoot` in `/etc/httpd/conf/httpd.conf` to point to `/opt/devweb/html`.  
🔸 I applied the correct SELinux file contexts using `semanage` and `restorecon`.  
🔸 I allowed HTTP traffic by opening port 80 using the firewall and reloaded the rules.

📸 **Deliverables**:
- Snippet of updated `httpd.conf` showing the new DocumentRoot
- Output of `ls -Z /opt/devweb/html` with SELinux contexts
- Output of `firewall-cmd --list-all`

---

## 📌 Phase 4: Scheduled Maintenance and Backup Automation

🗓️ **Context**:  
To ensure backups and scheduled tasks are functional, I implemented automation scripts and job scheduling.

🔸 I wrote a backup script `/opt/devweb/scripts/backup.sh` to copy `/opt/devweb/html` into `/opt/backup/` with a timestamp.  
🔸 I scheduled the script to run daily at 1 AM using `crontab` for the `devadmin` user.  
🔸 I created a one-time reboot job using the `at` command, scheduled to occur 10 minutes later.

📸 **Deliverables**:
- Output of `crontab -l -u devadmin`
- Contents of `backup.sh` script
- Output of `atq`

---

## 📌 Phase 5: Networking Configuration

🗓️ **Context**:  
I configured the server to use a static IP address and verified its connectivity.

🔸 I configured `eth0` with the static IP address `192.168.1.100/24` using `nmcli`.  
🔸 I set the DNS server to `8.8.8.8` in the same interface configuration.  
🔸 I verified the changes using `ip a`, tested DNS resolution with `ping`, and used `curl` to test local web access.

📸 **Deliverables**:
- Output of `ip a`
- Output of `nmcli con show`
- Contents of `/etc/hosts`
- Contents of `/etc/resolv.conf`

---

## 📌 Phase 6: Archiving and Logs

🗓️ **Context**:  
For log storage and cleanup, I implemented archiving and automatic log pruning.

🔸 I compressed the `/opt/devweb/logs` directory into `/tmp/devlogs.tar.gz` using `tar`.  
🔸 I scheduled a monthly cron job using `find` to delete log files older than 30 days.

📸 **Deliverables**:
- Output of `tar -tzf /tmp/devlogs.tar.gz`
- Cron job configuration
- `find` command used for cleanup

---

## 📌 Phase 7: SELinux and Service Management

🗓️ **Context**:  
I ensured SELinux was configured properly for persistent, secure web service access.

🔸 I verified SELinux was in enforcing mode using `getenforce`.  
🔸 I added a rule with `semanage fcontext` to label `/opt/devweb/html` with the correct context for Apache access.  
🔸 I applied the SELinux labels using `restorecon`.  
🔸 I ensured Apache is enabled to start on boot using `systemctl enable httpd`.

📸 **Deliverables**:
- Output of `getenforce`
- Output of `semanage fcontext` rule
- Output of `restorecon -Rv /opt/devweb/html`

---

## 📌 Phase 8: Troubleshooting and Logs

🗓️ **Context**:  
I simulated a service failure and practiced recovery techniques to build troubleshooting confidence.

🔸 I stopped Apache using `systemctl stop httpd` to simulate a failure.  
🔸 I viewed system logs using `journalctl -xe` and `/var/log/httpd/error_log` to identify the issue.  
🔸 I used `top` and `ps` to monitor processes and used `kill -9` to terminate a stuck process manually.

📸 **Deliverables**:
- Screenshot or logs of the Apache error
- Output showing use of `top`, `ps`, and `kill`
- Recovery steps and resolutions
