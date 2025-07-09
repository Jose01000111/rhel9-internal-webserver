# 🚀 Deploying and Managing a Departmental Web Server on RHEL 9

👨‍💻 **Role**: Junior System Administrator  
🏢 **Company**: DevCore Solutions  
📦 **Environment**: Red Hat Enterprise Linux 9
## 🧾 Introduction

As a junior system administrator at 🔵 **DevCore Solutions** , I have been tasked with designing, deploying, and managing a secure internal web server environment using **Red Hat Enterprise Linux 9 (RHEL 9)**. This project simulates real-world sysadmin responsibilities by walking through critical phases such as system setup, user and group management, web server configuration, security enforcement with SELinux, task automation, log handling, and network configuration.

| 📌 **Phase 1: Initial Setup and User Management**  |
|----------------------------------------------------|
| I began by installing RHEL 9 on the server, configuring essential system settings like hostname and timezone to fit our company standards. After updating the system to the latest packages, I created three user accounts (`devalpha`, `devbeta`, and `devadmin`) tailored for the development team. To streamline permissions management, I created a group called `developers` and added all these users to it. Finally, I secured administrative privileges by configuring `devadmin` with passwordless sudo access through a dedicated sudoers configuration file. |

📸 **Deliverables**:  
🟠 Screenshot of `/etc/passwd`  
🟠 Output of `id devalpha`  
🟠 Output of `sudo -l -U devadmin`


| 📌 **Phase 2: Directory and Permission Configuration**  |
|----------------------------------------------------------|
| With the users set up, I focused on building a clear directory structure under `/opt/devweb` to organize our web application files and support directories. I created subfolders for configuration files, logs, scripts, and HTML content. To facilitate collaborative work, I assigned group ownership of these directories to the `developers` group. Setting the SGID bit on the `scripts` directory ensured that all new files automatically inherit the group ownership, maintaining consistent access controls. |

📸 **Deliverables**:  
🟠 Output of `ls -lR /opt/devweb`  
🟠 Commands used for `chmod` and `chgrp`


| 📌 **Phase 3: Apache Installation and Configuration**  |
|---------------------------------------------------------|
| I installed the Apache HTTP server using the system’s package manager, then enabled and started its service to run on system boot. To serve the internal website, I created a simple `index.html` file in the `/opt/devweb/html` directory. I modified the Apache configuration to update the `DocumentRoot` to this new directory. Because SELinux is enforcing on the system, I configured the appropriate SELinux file contexts and applied them to the web directory. Lastly, I opened port 80 on the firewall to allow HTTP traffic. |

📸 **Deliverables**:  
🟠 Snippet of updated `httpd.conf` showing the new DocumentRoot  
🟠 Output of `ls -Z /opt/devweb/html` with SELinux contexts  
🟠 Output of `firewall-cmd --list-all`


| 📌 **Phase 4: Scheduled Maintenance and Backup Automation**  |
|--------------------------------------------------------------|
| To protect our web data, I developed a backup script that copies the website content to a backup directory with a timestamp for versioning. I scheduled this backup to run automatically every day at 1 AM using `crontab` under the `devadmin` user account. Additionally, I tested the scheduling system by creating a one-time `at` job to reboot the server after a 10-minute delay. |

📸 **Deliverables**:  
🟠 Output of `crontab -l -u devadmin`  
🟠 Contents of `backup.sh` script  
🟠 Output of `atq`


| 📌 **Phase 5: Networking Configuration**  |
|------------------------------------------|
| I configured the server’s primary network interface (`eth0`) to use a static IP address (`192.168.1.100/24`) and set the DNS resolver to Google’s public DNS (`8.8.8.8`) using NetworkManager’s CLI tools. To verify the network settings, I inspected the IP address assignment, checked active connections, tested connectivity to external hosts with `ping`, and confirmed local web access using `curl`. |

📸 **Deliverables**:  
🟠 Output of `ip a`  
🟠 Output of `nmcli con show`  
🟠 Contents of `/etc/hosts`  
🟠 Contents of `/etc/resolv.conf`


| 📌 **Phase 6: Archiving and Logs**  |
|------------------------------------|
| I archived the accumulated web server logs into a compressed tarball stored in `/tmp` for easier management and transfer. To prevent log accumulation from filling disk space, I set up a monthly cron job using the `find` command to delete log files older than 30 days, automating log maintenance. |

📸 **Deliverables**:  
🟠 Output of `tar -tzf /tmp/devlogs.tar.gz`  
🟠 Cron job configuration  
🟠 `find` command used for cleanup


| 📌 **Phase 7: SELinux and Service Management**  |
|-------------------------------------------------|
| SELinux enforcement was confirmed to be active, requiring that I configure appropriate security contexts for the custom web directory. Using `semanage fcontext`, I labeled `/opt/devweb/html` so Apache could access it without issues, and applied these labels with `restorecon`. To ensure the web server is always running after reboot, I enabled the `httpd` service to start on boot. |

📸 **Deliverables**:  
🟠 Output of `getenforce`  
🟠 Output of `semanage fcontext` rule  
🟠 Output of `restorecon -Rv /opt/devweb/html`


| 📌 **Phase 8: Troubleshooting and Logs**  |
|------------------------------------------|
| To prepare for real-world failures, I intentionally stopped the Apache service and examined the resulting error logs using both `journalctl` and the Apache error log file. I monitored running processes with `top` and `ps` and practiced terminating a stuck process using `kill -9` to ensure system stability and responsiveness. |

📸 **Deliverables**:  
🟠 Screenshot or logs of the Apache error  
🟠 Output showing use of `top`, `ps`, and `kill`  
🟠 Recovery steps and resolutions


## 🛠️ Technologies Used

| Technology                           | Description                                      |
|------------------------------------|------------------------------------------------|
| **Red Hat Enterprise Linux 9 (RHEL 9)** | Operating system for the server environment       |
| **Apache HTTP Server (httpd)**          | Web server software for hosting the internal website |
| **Bash Shell Scripting**                | Used for automation and backup scripts               |
| **SELinux**                            | Security module enforcing access controls            |
| **firewalld**                         | Firewall management tool to control network traffic  |
| **NetworkManager (nmcli)**             | CLI tool for network configuration                    |
| **Cron & At**                         | Job scheduling utilities for automation               |
| **Git & GitHub**                      | Version control and repository hosting                |


