# 🚀 Deploying and Managing a Departmental Web Server on RHEL 9

> 👨‍💻 **Role**: Junior System Administrator  
> 🏢 **Company**: DevCore Solutions  
> 📦 **Environment**: Red Hat Enterprise Linux 9 

## 🧾 Introduction

#### As a junior system administrator at **DevCore Solutions**, I have been tasked with designing, deploying, and managing a secure internal web server environment using **Red Hat Enterprise Linux 9 (RHEL 9)**. This project simulates real-world sysadmin responsibilities by walking through critical phases such as system setup, user and group management, web server configuration, security enforcement with SELinux, task automation, log handling, and network configuration.

---

| 📌 **Phase 1: Initial Setup and User Management**  |
|----------------------------------------------------|
| I began by installing RHEL 9 on the server, configuring essential system settings like hostname and timezone to fit our company standards. After updating the system to the latest packages, I created three user accounts (`devalpha`, `devbeta`, and `devadmin`) tailored for the development team. To streamline permissions management, I created a group called `developers` and added all these users to it. Finally, I secured administrative privileges by configuring `devadmin` with passwordless sudo access through a dedicated sudoers configuration file. |

### 🛠️ I set the hostname, timezone, and update the system. 

![ftnIULo](https://github.com/user-attachments/assets/e07e391b-0bb0-4ebb-a01b-d873ac6cae72)

### 🛠️ I create the users and the developers group, then add the users to the group.  

![wnQYbKX](https://github.com/user-attachments/assets/070a94c0-9883-4768-a689-4edeaca7b875)

### 🛠️ I give devadmin sudo access.

![o2YzwTy](https://github.com/user-attachments/assets/6b30ade4-2f0e-4012-a811-30932e62a3d5)

# 📸 **Deliverables**:  


### 🟠 Screenshot of `/etc/passwd`

![tH0qoxh](https://github.com/user-attachments/assets/cd491b2a-2fe3-458c-9fff-699df793b25f)

✅ Shows that the users exist

### 🟠 Output of `id devalpha`  

![bGNDjvL](https://github.com/user-attachments/assets/d3393fa9-4bde-48a1-aa3d-9d6d6cc30a4d)

✅ Verifies that devalpha is in the developers group

### 🟠 Output of `sudo -l -U devadmin`

![ozlFLf8](https://github.com/user-attachments/assets/4ea25ea4-40a4-4c49-8cd1-9c8a4528904c)

✅ Confirms devadmin has sudo privileges

---

| 📌 **Phase 2: Directory and Permission Configuration**  |
|----------------------------------------------------------|
| With the users set up, I focused on building a clear directory structure under `/opt/devweb` to organize our web application files and support directories. I created subfolders for configuration files, logs, scripts, and HTML content. To facilitate collaborative work, I assigned group ownership of these directories to the `developers` group. Setting the SGID bit on the `scripts` directory ensured that all new files automatically inherit the group ownership, maintaining consistent access controls. |

### 🛠️ I create the directory structure under `/opt/devweb`.  

![QXEkgHf](https://github.com/user-attachments/assets/f2598542-1001-49e0-b339-b188a5bc1f1f)

### 🛠️ I assign group ownership to the developers group.  

![1GxILvV](https://github.com/user-attachments/assets/8316d11c-5c19-4c5e-8668-53ab0e8c55c7)

# 📸 **Deliverables**:  
### 🟠 Output of `ls -lR /opt/devweb`  

![CJdn3oI](https://github.com/user-attachments/assets/d9d16c78-0370-4e83-81a7-2715dceb7381)

✅ Shows directory structure, group ownership, SGID

### 🟠 Commands used for `chmod` and `chgrp`

![bATijTK](https://github.com/user-attachments/assets/ea7580c3-98cb-49b8-baea-5a6b9fd86a56)

✅ Proof that permissions and group ownership were applied

---

| 📌 **Phase 3: Apache Installation and Configuration**  |
|---------------------------------------------------------|
| I installed the Apache HTTP server using the system’s package manager, then enabled and started its service to run on system boot. To serve the internal website, I created a simple `index.html` file in the `/opt/devweb/html` directory. I modified the Apache configuration to update the `DocumentRoot` to this new directory. Because SELinux is enforcing on the system, I configured the appropriate SELinux file contexts and applied them to the web directory. Lastly, I opened port 80 on the firewall to allow HTTP traffic. |

### 🛠️ I install and start the Apache web server.  

![CCODQwe](https://github.com/user-attachments/assets/58232e9e-72c1-444b-8ef1-df812d7145c3)

![TH6rzYz](https://github.com/user-attachments/assets/002b4363-efb1-423c-a773-377160a56ea4)

### 🛠️ I add a sample webpage to the `html` directory.  

![KTW1AFi](https://github.com/user-attachments/assets/d9738cc2-3b39-414f-8602-266b808ecdae)

### 🛠️ I update Apache’s DocumentRoot to point to the new `html` directory.  

![3sXMjmP](https://github.com/user-attachments/assets/c515cbda-ffc3-4813-9067-e6d061bbb8ce)

### 🛠️ I update the SELinux context for the new DocumentRoot.  

![tMRG4GT](https://github.com/user-attachments/assets/5cb9f33a-5360-4ac3-b9ba-27b0fd7307e4)

### 🛠️ I open port 80 in the firewall.

![rXVUHHA](https://github.com/user-attachments/assets/e126fd81-0589-4f8f-95ca-c3b8f10c9f2e)

# 📸 **Deliverables**:  
### 🟠 Snippet of updated `httpd.conf` showing the new DocumentRoot  

![MaIHec9](https://github.com/user-attachments/assets/766c7f91-209b-4812-8a21-83a6cbe3dbc2)

✅ Show the DocumentRoot now points to /opt/devweb/html

### 🟠 Output of `ls -Z /opt/devweb/html` with SELinux contexts  

![mfnzzAG](https://github.com/user-attachments/assets/908ea5d2-6244-48d3-8bdd-f191dfcef652)

✅ Shows correct SELinux label (httpd_sys_content_t)

### 🟠 Output of `firewall-cmd --list-all`

![Ji2SlEt](https://github.com/user-attachments/assets/5adf5ed3-7981-4d01-a5b4-690aa5b796dd)

✅ Shows that port 80 is open

---

| 📌 **Phase 4: Scheduled Maintenance and Backup Automation**  |
|--------------------------------------------------------------|
| To protect our web data, I developed a backup script that copies the website content to a backup directory with a timestamp for versioning. I scheduled this backup to run automatically every day at 1 AM using `crontab` under the `devadmin` user account. Additionally, I tested the scheduling system by creating a one-time `at` job to reboot the server after a 10-minute delay. |

### 🛠️ I create a backup script that copies the `html` directory with a date stamp.  

![R5BS56x](https://github.com/user-attachments/assets/7a26f9c6-813e-4c8d-a430-b6af7d320d4f)

### 🛠️ I schedule the backup script to run daily as the `devadmin` user.  

![XcfccEH](https://github.com/user-attachments/assets/3c47c8e3-3fc6-45a0-9c67-5bd3d64da8f5)

### 🛠️ I schedule a reboot to occur in 10 minutes using an at job.

![RFmbisC](https://github.com/user-attachments/assets/3a3215ef-0baa-4cdc-b823-f1d7900e3980)

# 📸 **Deliverables**:  
### 🟠 Output of `crontab -l -u devadmin`  

![hrc66Np](https://github.com/user-attachments/assets/7658229a-7dbb-4daa-ae7f-e7d3952d1140)


✅ Shows script content

### 🟠 Contents of `backup.sh` script 

![9fbD7CQ](https://github.com/user-attachments/assets/7cf2d53e-cbee-4d32-ad70-a0b528c8c8fd)

✅ Confirms cron is scheduled

### 🟠 Output of `atq`

![ouX1Ri8](https://github.com/user-attachments/assets/b0bc5c52-d973-4602-ad2a-4a42a58e4a3b)

✅ Shows scheduled reboot

---

| 📌 **Phase 5: Networking Configuration**  |
|------------------------------------------|
| I configured the server’s primary network interface (`eth0`) to use a static IP address (`192.168.1.100/24`) and set the DNS resolver to Google’s public DNS (`8.8.8.8`) using NetworkManager’s CLI tools. To verify the network settings, I inspected the IP address assignment, checked active connections, tested connectivity to external hosts with `ping`, and confirmed local web access using `curl`. |

### 🛠️ I assign a static IP address and set DNS for the network interface.  

![oAH6E4s](https://github.com/user-attachments/assets/a0ee8da1-3975-48ce-9757-f848bfd39479)

### 🛠️ I verify network connectivity and web service availability.

![5s1RJQt](https://github.com/user-attachments/assets/afc18c94-ef1d-412c-88d0-97713a8e5c91)

# 📸 **Deliverables**:  
### 🟠 Output of `ip a`  

![Ma2t2Sw](https://github.com/user-attachments/assets/023db2b3-8e40-4beb-9205-33ed1ff3419a)

✅ Shows IP 192.168.1.100 on eth0

### 🟠 Output of `nmcli con show` 

![eB9ZOVV](https://github.com/user-attachments/assets/2039df18-0e10-4631-abaf-f8aae838c84e)

✅ Shows static IP and DNS settings

### 🟠 Contents of `/etc/hosts`  

![DlGah4Q](https://github.com/user-attachments/assets/1b3e886b-ad2f-4c81-b53d-93c5c47afed0)

✅ Shows correct hostname/IP mapping

### 🟠 Contents of `/etc/resolv.conf`

![BdQIcWK](https://github.com/user-attachments/assets/cd446d19-18f3-4843-80b2-9ed09d0c2868)

✅ Shows 8.8.8.8 as DNS

---

| 📌 **Phase 6: Archiving and Logs**  |
|------------------------------------|
| I archived the accumulated web server logs into a compressed tarball stored in `/tmp` for easier management and transfer. To prevent log accumulation from filling disk space, I set up a monthly cron job using the `find` command to delete log files older than 30 days, automating log maintenance. |

### 🛠️ I archive the logs directory into a compressed tarball.  

![K4rvvXZ](https://github.com/user-attachments/assets/af67a53a-3776-4a3c-aba5-a3754e1151d9)

### 🛠️ I schedule a monthly cleanup to delete logs older than 30 days.

![vQymTl0](https://github.com/user-attachments/assets/1666fe2d-2fb4-4e3d-84a3-ca87ecb2d9a9)

# 📸 **Deliverables**:  
### 🟠 Output of `tar -tzf /tmp/devlogs.tar.gz`  

![uIGpPyH](https://github.com/user-attachments/assets/6555a742-4ebe-4dec-87b4-4145aee3d42f)

✅ Shows contents of archive

### 🟠 Cron job configuration 

![mVpJDrK](https://github.com/user-attachments/assets/ae781c9a-779b-43c7-8880-1fba40550ec9)

✅ Shows cleanup cron job

### 🟠 `find` command used for cleanup

![q2umfsi](https://github.com/user-attachments/assets/b67ac943-b315-44a4-adcd-6b338667f329)

✅ Shows correct cleanup command

---

| 📌 **Phase 7: SELinux and Service Management**  |
|-------------------------------------------------|
| SELinux enforcement was confirmed to be active, requiring that I configure appropriate security contexts for the custom web directory. Using `semanage fcontext`, I labeled `/opt/devweb/html` so Apache could access it without issues, and applied these labels with `restorecon`. To ensure the web server is always running after reboot, I enabled the `httpd` service to start on boot. |

### 🛠️ I check that SELinux is enabled and enforcing.  
### 🛠️ I add SELinux rules to allow Apache to access the new DocumentRoot and restore contexts.  
### 🛠️ I restart Apache and enable it to start on boot.

# 📸 **Deliverables**:  
### 🟠 Output of `getenforce`  

![ZiLUlux](https://github.com/user-attachments/assets/0618feef-4c4f-4133-987c-f75a7aba861d)

✅ Shows mode is Enforcing

### 🟠 Output of `semanage fcontext` rule  

![EoNpX2l](https://github.com/user-attachments/assets/076e97b8-005f-4224-8cf9-25a59c62aa40)

✅ Shows new SELinux rule

![9h4UNHk](https://github.com/user-attachments/assets/3a2dcdcd-f9fe-417c-9c4b-fdfa7645b952)

### 🟠 Output of `restorecon -Rv /opt/devweb/html`

![EoNpX2l](https://github.com/user-attachments/assets/d291fa4d-9478-46c7-8d93-280bc5fd82b3)

✅ Shows relabeling of directory

---

| 📌 **Phase 8: Troubleshooting and Logs**  |
|------------------------------------------|
| To prepare for real-world failures, I intentionally stopped the Apache service and examined the resulting error logs using both `journalctl` and the Apache error log file. I monitored running processes with `top` and `ps` and practiced terminating a stuck process using `kill -9` to ensure system stability and responsiveness. |

### 🛠️ I simulate a failure by stopping the Apache service.  

![He3smWn](https://github.com/user-attachments/assets/71f2f53b-de79-4fcb-a2d8-e0a4ff141cc5)

### 🛠️ I review logs to diagnose the problem.  

![7okIEYv](https://github.com/user-attachments/assets/2802ccf3-8817-44c2-80e0-b70959717aeb)

### 🛠️ I use system tools to find and kill any stuck processes.

![dnAHqVH](https://github.com/user-attachments/assets/30badcb0-79d2-4b23-9360-aa922c366bcd)

# 📸 **Deliverables**:  
### 🟠 Screenshot or logs of the Apache error  

![He3smWn](https://github.com/user-attachments/assets/71f2f53b-de79-4fcb-a2d8-e0a4ff141cc5)

✅ Output from journalctl -xe showing the Apache failure

### 🟠 Output showing use of `top`, `ps`, and `kill`  

![dnAHqVH](https://github.com/user-attachments/assets/2117fe82-34ca-41eb-901b-3b65940c04be)

![7okIEYv](https://github.com/user-attachments/assets/fe302aeb-8ef1-4a06-8dc9-f51c474c1e5b)

![OQgm6TN](https://github.com/user-attachments/assets/0432e3c9-41fe-43e2-adae-218560ccfe79)

✅ Demonstrate using top, ps aux | grep httpd, and sudo kill -9 1

### 🟠 Recovery steps and resolutions

![rgLCodl](https://github.com/user-attachments/assets/2382685a-0839-4e1a-a79d-e1a690a668b1)

✅ Contents of /var/log/httpd/error_log showing detailed Apache error logs

---

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


