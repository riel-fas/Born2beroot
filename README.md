� Born2beroot - 42 School Project
<p align="center"> <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/8d/42_Logo.svg/1200px-42_Logo.svg.png" alt="42 Logo" width="150"/> <img src="https://www.1337.ma/wp-content/uploads/2021/04/1337_logo.png" alt="1337 Logo" width="150"/> </p>
A secure virtual machine setup with Debian/Rocky Linux, LSM, UFW, SSH, and password policies as part of the 42 School curriculum.

🌈 Table of Contents
💿 Virtual Machine

1.1 Virtualization & Hypervisor (VMM)

1.2 VDI Files

1.3 Debian Linux

1.4 Rocky Linux

1.5 Debian vs Rocky

🛠 Linux Security Module (LSM)

📦 Aptitude & APT

⚙️ Virtual Machine Setup

4.1 Installing sudo & User/Groups

4.2 Installing & Configuring SSH

4.3 Installing & Configuring UFW

4.4 Sudo Policies

4.5 Strong Password Policy

4.6 Connecting via SSH

🚨 Monitoring Script

5.1 Script Output

⏰ Crontab

📝 Signature.txt

⭐ Bonus

8.1 Manual Partition

8.2 WordPress & Services

8.3 Additional Service

✅ Correction Sheet

9.1 Evaluation Answers

9.2 Evaluation Commands

1️⃣ 💿 Virtual Machine
1.1 Virtualization & Hypervisor (VMM)
🔹 Type-1 (Bare-metal): VMware ESXi, Hyper-V
🔹 Type-2 (Hosted): VirtualBox, QEMU

1.2 VDI Files
📁 Virtual Disk Image (VDI) is VirtualBox’s native format.

1.3 Debian Linux
🐧 Stable, lightweight, preferred for servers.

1.4 Rocky Linux
🪨 RHEL-compatible, enterprise-grade.

1.5 Debian vs Rocky
Feature	Debian 🟢	Rocky 🟠
Package Manager	APT	DNF
Stability	High	Very High
Use Case	Servers	Enterprise
2️⃣ 🛠 Linux Security Module (LSM)
🔒 AppArmor (Debian default) vs SELinux (Rocky default).

3️⃣ 📦 Aptitude & APT
bash
Copy
sudo apt update && sudo apt upgrade -y
4️⃣ ⚙️ Virtual Machine Setup
4.1 Installing sudo & Users/Groups
bash
Copy
adduser <username>
usermod -aG sudo <username>
4.2 SSH Configuration
bash
Copy
sudo apt install openssh-server
sudo systemctl enable --now ssh
4.3 UFW Firewall
bash
Copy
sudo ufw allow 4242
sudo ufw enable
4.4 Sudo Policies
Edit /etc/sudoers with visudo.

4.5 Password Policy
bash
Copy
sudo vi /etc/login.defs  # Set PASS_MAX_DAYS, PASS_MIN_DAYS, etc.
4.6 SSH Connection
bash
Copy
ssh <user>@<ip> -p 4242
5️⃣ 🚨 Monitoring Script
📊 Displays:

CPU, RAM, Disk Usage

Network Stats

Output Example:

Copy
-------------------------------------
| CPU Usage: 15%                    |
| Memory Usage: 30%                 |
| Disk Usage: 45%                   |
-------------------------------------
6️⃣ ⏰ Crontab
bash
Copy
crontab -e
# Add: */10 * * * * /path/to/monitoring_script.sh
7️⃣ 📝 Signature.txt
bash
Copy
shasum <your_vm>.vdi > signature.txt
8️⃣ ⭐ Bonus
8.1 Manual Partition
🗂 Required partitions: /, /home, /var, /tmp, /boot.

8.2 WordPress Setup
🌐 LAMP Stack: Apache, MySQL, PHP.

8.3 Additional Service
🛡 Fail2Ban for SSH protection.

9️⃣ ✅ Correction Sheet
9.1 Evaluation Answers
📋 Expected responses for the defense.

9.2 Evaluation Commands
bash
Copy
uname -a  # Check OS
sudo ufw status  # Check firewall
<p align="center"> <img src="https://img.shields.io/badge/42-Born2beroot-blue" alt="42 Born2beroot Badge"/> <img src="https://img.shields.io/badge/1337-Project-green" alt="1337 Project Badge"/> </p>
