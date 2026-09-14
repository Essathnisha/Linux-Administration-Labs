📊 Linux Log Monitoring & Rotation

> A hands-on Linux System Administration project focused on log monitoring, disk usage analysis, and automated log rotation.

---

📌 Project Overview

Linux servers continuously generate system, service, and application logs. If these logs are not managed properly, they can consume disk space and affect server performance.

In this project, I monitored Linux logs, analyzed log disk usage, created a custom application log, configured `logrotate`, tested the configuration safely, and verified successful log rotation and compression.

---

🎯 Objectives

- Monitor system logs
- Monitor SSH service logs
- Analyze `/var/log` disk usage
- Understand Linux logrotate configuration
- Create an application log file
- Configure custom log rotation
- Compress old log files
- Manage log retention
- Perform safe configuration testing
- Verify successful log rotation

---

🛠️ Technologies & Tools

| Tool | Purpose |
|------|---------|
| Ubuntu Linux | Operating System |
| Bash | Command-line administration |
| tail | System log monitoring |
| journalctl | Service log monitoring |
| du | Disk usage analysis |
| logrotate | Log rotation |
| gzip | Log compression |
| systemctl | Service management |

---

🔧 Implementation

 1️⃣ Monitor System Logs

 bash
sudo tail -20 /var/log/syslog

Purpose:
Displays the latest 20 lines of the system log to monitor recent system activity, errors, warnings, and events.


---

2️⃣ Monitor SSH Service Logs

sudo journalctl -u ssh --since "1 hour ago"

Purpose:
Checks SSH service activity and helps troubleshoot SSH-related issues.

Command Options:

journalctl → Reads systemd journal logs

-u → Specifies a service/unit

--since → Shows logs from a specified time



---

3️⃣ Check Log Disk Usage

du -sh /var/log

Purpose:
Checks how much disk space is being consumed by Linux log files.

Command Options:

du → Disk usage

-s → Summary

-h → Human-readable format



---

4️⃣ Review Default Logrotate Configuration

cat /etc/logrotate.conf

Purpose:
Reviews the default Linux log rotation configuration and helps understand how system logs are managed.


---

5️⃣ Create a Test Application Log

sudo mkdir -p /var/log/myapp

sudo touch /var/log/myapp/app.log

echo "Test log entry" | sudo tee -a /var/log/myapp/app.log

Purpose:
Creates a sample application log file to demonstrate custom log rotation.


---

6️⃣ Configure Custom Log Rotation

Create a custom configuration file:

sudo nano /etc/logrotate.d/myapp

Add:

/var/log/myapp/app.log {
    daily
    rotate 7
    compress
    missingok
    notifempty
}

Configuration

Option	Description

daily	Rotates the log daily
rotate 7	Keeps 7 rotated log copies
compress	Compresses old log files
missingok	Ignores missing log files
notifempty	Does not rotate empty logs


Purpose:
Creates an application-specific log rotation policy to control log growth and disk usage.


---

7️⃣ Safely Test the Configuration

sudo logrotate -d /etc/logrotate.d/myapp

Purpose:
Tests the configuration in debug mode without actually performing log rotation.

-d → Debug mode


---

8️⃣ Force Log Rotation & Verify

sudo logrotate -f /etc/logrotate.d/myapp

ls -la /var/log/myapp/

Purpose:
Forces log rotation and verifies that the rotated log files were created successfully.

-f → Forces log rotation

Expected Result

app.log
app.log.1.gz

The .gz file indicates that the rotated log has been compressed.


---

🔄 Log Rotation Workflow

Application

     ↓
  app.log
  
     ↓
 Logrotate
 
     ↓
Daily Rotation

     ↓
Compression

     ↓
Keep 7 Copies

     ↓
Remove Older Logs

     ↓
Controlled Disk Usage


---

🔒 Key Features

✅ System log monitoring

✅ SSH service log monitoring

✅ Disk usage monitoring

✅ Custom logrotate configuration

✅ Application-specific log management

✅ Automatic log compression

✅ Log retention management

✅ Safe dry-run testing

✅ Log rotation verification


---

💼 Real-World Applications

🖥️ Production Linux Servers

Log rotation prevents continuously growing logs from consuming all available disk space.

🌐 Web Servers

Nginx and Apache generate access and error logs continuously. Log rotation helps manage these logs efficiently.

⚙️ Application Servers

Custom logrotate rules can be created for application-specific log files.

☁️ AWS EC2

Linux servers running on AWS EC2 can use log monitoring and rotation to maintain healthy disk usage.

🔍 Troubleshooting

System and service logs help administrators identify errors, failed services, and unexpected system activity.

💾 Disk Space Management

Compression and retention policies reduce unnecessary disk consumption.


---
😻
🧪 Testing & Verification

The following tasks were successfully performed:

[x] System log monitoring

[x] SSH service log monitoring

[x] Log disk usage analysis

[x] Default logrotate configuration review

[x] Test application log creation

[x] Custom logrotate configuration

[x] Dry-run testing

[x] Forced log rotation

[x] Compressed log verification



---

📸 Project Evidence

Screenshots of the practical implementation are available in the screenshots directory.

Evidence Includes

1. System log monitoring


2. SSH service logs


3. Log disk usage


4. Default logrotate configuration


5. Test application log


6. Custom logrotate rule


7. Logrotate dry-run output


8. Successful log rotation




---

📚 Key Learning Outcomes

Through this project, I gained practical experience in:

Linux log monitoring

Systemd journal management

Disk usage analysis

Logrotate configuration

Log compression

Log retention management

Linux troubleshooting

Server maintenance

Basic Linux system administration



---

👩‍💻 Project Author

Essath Nisha E

BCA Graduate | Linux Administration | AWS Cloud Support


---

⚠️ Disclaimer

This project was created for learning and practical demonstration purposes. Log rotation policies should be reviewed and adjusted according to the requirements of each production environment.
