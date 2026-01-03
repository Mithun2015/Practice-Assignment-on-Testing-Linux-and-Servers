# Practice-Assignment-on-Testing-Linux-and-Servers
Practice Assignment on Testing, Linux and Servers

1-System Monitoring Setup
2-User Management and Access Control
3-Backup Configuration for Web Servers


# Project Name:Practice-Assignment-on-Testing-Linux-and-Servers

## Overview
Task 1: System Monitoring Setup

Install and configure htop or nmon to monitor CPU, memory, and processes, using df and du for disk usage tracking, and identifying resource-intensive processes. Proper logging of system metrics and clear documentation of the setup are essential. 

Task 2: User Management and Access Control

Evaluation includes creating user accounts for Sarah and Mike with secure passwords, setting up isolated directories with appropriate permissions, and enforcing a password policy with expiration and complexity. Detailed documentation of user management steps is required. 

Task 3: Backup Configuration for Web Servers

Configure automated backups for Apache (/etc/httpd/, /var/www/html/) and Nginx (/etc/nginx/, /usr/share/nginx/html/), scheduling cron jobs to run every Tuesday at 12:00 AM, using the correct naming convention for backup files, and verifying backup integrity. Proper documentation and logs are necessary. 

Overall Report and Presentation

The report should clearly summarize implementation steps and challenges, including relevant screenshots or terminal outputs demonstrating task completion.




## Prerequisites
os Platform :ubuntu
Tools:htop,nmon,cron,nano

## Installation
Install Monitoring Tools
root@0cbb92052029:/# apt update
root@0cbb92052029:/# apt install htop -y
root@0cbb92052029:/# apt install nmon -y  
<img width="736" height="118" alt="image" src="https://github.com/user-attachments/assets/1242d918-41bd-4b92-b279-76ccb1117805" />



## Usage
Starting htop
root@0cbb92052029:/# htop<img width="486" height="92" alt="image" src="https://github.com/user-attachments/assets/d5a2dc5d-6f95-453e-a096-91e36d3db66b" />
Starting nmon
root@0cbb92052029:/# nmon<img width="486" height="64" alt="image" src="https://github.com/user-attachments/assets/eee0d00a-4120-46ef-934d-ee722cff537e" />

USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0   4296  3572 pts/0    Ss   04:01   0:00 /bin/bash
root       240 50.0  0.0   7628  3444 pts/0    R+   04:17   0:00 ps aux --sort=-%mem
root       241  0.0  0.0   2280  1076 pts/0    S+   04:17   0:00 head
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0   4296  3572 pts/0    Ss   04:01   0:00 /bin/bash
root       242  0.0  0.0   7628  3444 pts/0    R+   04:17   0:00 ps aux --sort=-%cpu
root       243  0.0  0.0   2280  1068 pts/0    S+   04:17   0:00 head



root@0cbb92052029:/# mkdir -p /var/log/system_monitoring
nano /usr/local/bin/system_monitor.sh



root@0cbb92052029:/# chmod +x /usr/local/bin/system_monitor.sh

root@0cbb92052029:/# crontab -e




<img width="1336" height="938" alt="image" src="https://github.com/user-attachments/assets/b4b1bb0d-3395-4aff-90e6-7da81d642014" />



User Management and Access Control
Create User Accounts
root@0cbb92052029:/# useradd sarah
root@0cbb92052029:/# useradd mike

root@0cbb92052029:/# id sarah
uid=1001(sarah) gid=1001(sarah) groups=1001(sarah)
root@0cbb92052029:/# id mike 
uid=1002(mike) gid=1002(mike) groups=1002(mike)
root@0cbb92052029:/# 

Set passwords
root@0cbb92052029:/# passwd sarah
New password: 
Retype new password: 
passwd: password updated successfully
root@0cbb92052029:/# 

root@0cbb92052029:/# passwd mike    
New password: 
Retype new password: 
passwd: password updated successfully
root@0cbb92052029:/# 

Create Isolated Working Directories
root@0cbb92052029:/# mkdir -p /home/sarah/workspace
mkdir -p /home/mike/workspace
root@0cbb92052029:/# 

Assign ownership
root@0cbb92052029:/# chown -R sarah:sarah /home/sarah
chown -R mike:mike /home/mike
root@0cbb92052029:/# 

Set permissions:
root@0cbb92052029:/# chmod 700 /home/sarah/workspace
chmod 700 /home/mike/workspace

root@0cbb92052029:/# ls -ld /home/*/workspace
drwx------ 2 mike  mike  4096 Jan  3 10:00 /home/mike/workspace
drwx------ 2 sarah sarah 4096 Jan  3 10:00 /home/sarah/workspace


Enforce Password Expiration Policy
Set password expiration to 30 days
root@0cbb92052029:/# chage -M 30 sarah
chage -M 30 mike
root@0cbb92052029:/# 

Verify
root@0cbb92052029:/# chage -l sarah
chage -l mike
Last password change					: Jan 03, 2026
Password expires					: Feb 02, 2026
Password inactive					: never
Account expires						: never
Minimum number of days between password change		: 0
Maximum number of days between password change		: 30
Number of days of warning before password expires	: 7
Last password change					: Jan 03, 2026
Password expires					: Feb 02, 2026
Password inactive					: never
Account expires						: never
Minimum number of days between password change		: 0
Maximum number of days between password change		: 30
Number of days of warning before password expires	: 7

Enforce Password Complexity
root@0cbb92052029:/# nano /etc/security/pwquality.conf




Backup Configuration for Web Servers
Create Backup Directory
root@0cbb92052029:/# mkdir /backups
chmod 755 /backups

Backup Script for Apache (Sarah)
Create script
root@0cbb92052029:/# nano /usr/local/bin/apache_backup.sh

Script Executable
root@0cbb92052029:/# chmod +x /usr/local/bin/apache_backup.sh

Backup Script for Nginx (Mike)
root@0cbb92052029:/# nano /usr/local/bin/nginx_backup.sh

Script Executable
oot@0cbb92052029:/# chmod +x /usr/local/bin/nginx_backup.sh

Schedule Cron Jobs (Every Tuesday at 12:00 AM)
root@0cbb92052029:/# crontab -e



Verify Backups Manually
root@0cbb92052029:/# ls -ld /backups
drwxr-xr-x 2 root root 4096 Jan  3 10:06 /backups

root@0cbb92052029:/# ls -lh /backups/
total 0

root@0cbb92052029:/# mkdir -p /backups
root@0cbb92052029:/# date +%F
2026-01-03

<img width="1096" height="4168" alt="image" src="https://github.com/user-attachments/assets/81697060-5f39-4a53-baed-d14a401e5744" />


