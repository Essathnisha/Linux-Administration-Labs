🔐 Linux Secure Server Setup

📌 Project Overview

A hands-on Linux project focused on securing a Linux server using basic system administration and security practices.

This project demonstrates how to create a restricted user account, manage users through groups, configure file permissions, secure SSH access, enable a firewall, and implement passwordless SSH login using SSH keys.

The objective is to improve server security by restricting unauthorized access and allowing only required users and services.

---

🎯 Project Objectives

- Create and manage Linux users
- Create groups and assign users based on roles
- Configure file and directory permissions
- Install and manage SSH service
- Harden SSH configuration
- Configure UFW firewall
- Generate SSH key pairs
- Configure passwordless SSH authentication
- Test and verify secure server access

---

🏗️ Architecture

                    Linux Secure Server
                           │
             ┌─────────────┴─────────────┐
             │                           │
       User Management              SSH Security
             │                           │
     devuser + developers        SSH Key Authentication
             │                           │
             ▼                           ▼
      /project-data              Passwordless Login
        chmod 770                       │
             │                          │
             └────────────┬─────────────┘
                          ▼
                    UFW Firewall
                          │
                          ▼
                  Secure Linux Server

---

🛠️ Implementation Steps

Step 1: Create a New User

sudo adduser devuser

Commands:

- "sudo" → SuperUser DO; runs commands with administrator privileges
- "adduser" → Creates a new Linux user

Use Case:

Creates a separate login account for an employee or administrator instead of allowing everyone to share the same account.

---

Step 2: Create a Group and Add the User

sudo groupadd developers
sudo usermod -aG developers devuser
groups devuser

Commands:

- "groupadd" → Creates a new group
- "usermod -aG" → Adds a user to an additional group
- "groups" → Displays the groups a user belongs to

Use Case:

Role-based access can be managed through groups. Instead of assigning permissions individually, the same permissions can be given to all members of the "developers" group.

---

Step 3: Create a Folder and Set Permissions

sudo mkdir /project-data
sudo chown devuser:developers /project-data
sudo chmod 770 /project-data
ls -ld /project-data

Commands:

- "mkdir" → Creates a directory
- "chown" → Changes owner and group ownership
- "chmod" → Changes file or directory permissions
- "ls -ld" → Displays directory details and permissions

Use Case:

Restricts access to the project directory so that only the owner and members of the assigned group can access it.

Permission Model

770

Owner  → Read + Write + Execute
Group  → Read + Write + Execute
Others → No Access

---

Step 4: Install and Start the SSH Server

sudo apt update
sudo apt install openssh-server -y
sudo systemctl start ssh
sudo systemctl enable ssh

Commands:

- "apt" → Advanced Package Tool used for package management
- "systemctl" → Manages Linux system services

Use Case:

Enables the Linux server to accept remote SSH connections for secure administration.

---

Step 5: Harden the SSH Configuration

Edit the SSH configuration file:

sudo nano /etc/ssh/sshd_config

Security settings:

PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes

Restart SSH:

sudo systemctl restart ssh

Security Purpose

PermitRootLogin no

Prevents direct SSH login using the root account.

PasswordAuthentication no

Disables password-based SSH authentication and requires key-based authentication.

PubkeyAuthentication yes

Enables SSH public-key authentication.

Use Case:

Reduces the risk of unauthorized access and password-based brute-force attacks on SSH.

«⚠️ Password authentication should only be disabled after confirming that key-based SSH login works, otherwise remote access can be locked out.»

---

Step 6: Enable the Firewall (UFW)

sudo ufw allow ssh
sudo ufw enable
sudo ufw status

Commands:

- "ufw" → Uncomplicated Firewall
- "allow" → Permits specified traffic
- "status" → Displays firewall rules and status

Use Case:

Controls incoming network traffic and allows only the services that are required.

Expected Security Concept

Internet
    │
    ▼
 UFW Firewall
    │
    ├── SSH → Allowed
    │
    └── Unwanted Traffic → Blocked

---

Step 7: Generate an SSH Key for Passwordless Login

Switch to the "devuser" account:

sudo su - devuser

Generate an SSH key pair:

ssh-keygen -t rsa -b 4096

Add the public key to the authorized keys file:

cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

Set secure permissions:

chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys

Commands:

- "su" → Switch User
- "ssh-keygen" → Generates an SSH key pair
- "-t rsa" → Specifies RSA key type
- "-b 4096" → Uses a 4096-bit RSA key
- "cat ... >>" → Appends the public key to "authorized_keys"

Use Case:

Allows SSH authentication using cryptographic keys instead of relying on a password.

---

Step 8: Test the Login

ssh devuser@localhost

Commands:

- "ssh" → Secure Shell
- "localhost" → Refers to the same Linux machine

Expected Result

The "devuser" account should successfully connect through SSH using the configured SSH key without requesting a password.

Use Case:

Verifies that the complete SSH security and passwordless authentication configuration is working correctly.

---

🔒 Security Features Implemented

- ✅ Dedicated user account
- ✅ Group-based access control
- ✅ Restricted directory permissions
- ✅ Root SSH login disabled
- ✅ Password-based SSH authentication disabled
- ✅ SSH public-key authentication enabled
- ✅ UFW firewall enabled
- ✅ Passwordless SSH login
- ✅ Secure ".ssh" directory permissions

---

💼 Real-World Use Cases

1. Linux Server Administration

System administrators can securely manage Linux servers using SSH instead of direct physical access.

2. Employee Access Management

Separate user accounts can be created for employees instead of sharing a common administrator account.

3. Role-Based Access Control

Groups can be used to provide the same access permissions to users with the same job role.

4. Web/Application Servers

Sensitive application directories can be protected using Linux ownership and permission controls.

5. Cloud Servers

These security practices can be applied to Linux cloud instances such as AWS EC2.

6. Server Hardening

SSH hardening and firewall configuration help reduce common unauthorized-access risks.

---

🧪 Testing & Verification

The following configurations were tested:

✓ User creation
✓ Group membership
✓ Directory ownership
✓ File permissions
✓ SSH service
✓ SSH configuration
✓ UFW firewall
✓ SSH key authentication
✓ Passwordless SSH login

---

📸 Project Evidence

Screenshots are included to demonstrate the practical implementation.

Recommended screenshots:

screenshots/
│
├── user-created.png
├── group-membership.png
├── directory-permissions.png
├── ssh-status.png
├── ssh-hardening.png
├── ufw-status.png
├── ssh-key.png
└── passwordless-login.png

---

📚 Key Learning Outcomes

Through this project, I gained practical experience in:

- Linux user and group management
- Linux file permissions
- SSH administration
- SSH security hardening
- Firewall configuration
- Public-key authentication
- Passwordless SSH
- Basic Linux server security
- Linux system administration

---

👩‍💻 Project Author

Essath Nisha E

BCA Graduate | Linux Administration | AWS Cloud Support
