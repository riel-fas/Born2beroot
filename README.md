<p align="center"> <img src="https://img.shields.io/badge/OS-Debian/CentOS-blue?style=for-the-badge&logo=linux" alt="OS"> <img src="https://img.shields.io/badge/VirtualBox-UTM-orange?style=for-the-badge&logo=virtualbox" alt="VirtualBox"> <img src="https://img.shields.io/badge/Status-Completed-success?style=for-the-badge" alt="Status"> </p> <h1 align="center">🚀 Born2beroot 🚀</h1> <p align="center"> <i>A system administration project from 42 School where you configure a secure virtual machine using Debian or CentOS.</i> </p>

---

## 📖 Table of Contents
1. [Introduction](#introduction)
2. [What is a Virtual Machine?](#what-is-a-virtual-machine)
3. [How do Virtual Machines Work?](#how-do-virtual-machines-work)
4. [What is LVM?](#what-is-lvm)
5. [What is AppArmor?](#what-is-apparmor)
6. [Difference Between Apt and Aptitude](#difference-between-apt-and-aptitude)
7. [What is SSH?](#what-is-ssh)
8. [What is UFW and How to Implement UFW with SSH?](#what-is-ufw-and-how-to-implement-ufw-with-ssh)
9. [What is cron and what is wall?](#what-is-cron-and-what-is-wall)
10. [Installation](#installation)
11. [sudo Configuration](#sudo-configuration)
    - [Step 1: Installing sudo](#step-1-installing-sudo)
    - [Step 2: Adding User to sudo Group](#step-2-adding-user-to-sudo-group)
    - [Step 3: Running root-Privileged Commands](#step-3-running-root-privileged-commands)
    - [Step 4: Configuring sudo](#step-4-configuring-sudo)
12. [SSH Configuration](#ssh-configuration)
    - [Step 1: Installing & Configuring SSH](#step-1-installing--configuring-ssh)
    - [Step 2: Installing & Configuring UFW](#step-2-installing--configuring-ufw)
    - [Step 3: Connecting via SSH](#step-3-connecting-via-ssh)
13. [User Management](#user-management)
    - [Step 1: Password Policy](#step-1-password-policy)
    - [Step 2: Creating a New User](#step-2-creating-a-new-user)
    - [Step 3: Creating a New Group](#step-3-creating-a-new-group)
14. [cron Configuration](#cron-configuration)
15. [Monitoring Script](#monitoring-script)
16. [Bonus](#bonus)
    - [WordPress Installation](#wordpress-installation)
    - [FTP Configuration](#ftp-configuration)
17. [Submission](#submission)
18. [Evaluation Knowledge](#evaluation-knowledge)

---

## 🖥️ Introduction

Born2beroot is a system administration project from 42 School. The goal of this project is to create a secure virtual machine using Debian or Rocky within a virtual environment like VirtualBox or UTM.

🔍 What You'll Do:

✅ Set up user privileges and security measures

✅ Configure SSH access and firewall rules

✅ Set up password policies and sudo configuration

✅ Monitor system resources and automate services


This README will guide you through the setup process step-by-step to help you build a functional and secure server environment.

---

### What is a Virtual Machine?
A Virtual Machine (VM) is a software-based emulation of a physical computer. It allows you to run an operating system (OS) within another OS. VMs are highly versatile and commonly used for purposes such as testing, development, and server management.

---

### How do Virtual Machines Work?
Virtual Machines operate through the use of a hypervisor, a type of software responsible for creating and managing virtual environments. The hypervisor allocates resources, including CPU, RAM, and storage, from the host machine to the VM. This enables the VM to function as an independent system, separate from the host operating system.

Key Properties:

➡️ Hypervisor: Software (e.g., VirtualBox, UTM) that creates/manages VMs.

➡️ Isolation: VM crashes won’t affect the host machine.

➡️ Snapshots: Save/restore VM state at any point.


Types of VMs:

➡️ Type 1 (Bare-metal): Runs directly on hardware (e.g., VMware ESXi).

➡️ Type 2 (Hosted): Runs on top of an OS (e.g., VirtualBox).

---

### What is LVM?

Logical Volume Manager (LVM) is an advanced storage management system designed to provide flexibility and efficiency in managing disk storage. Unlike traditional partitioning methods that are fixed in size and structure, LVM introduces a dynamic approach by abstracting physical disks into logical volumes.

#### Key Features of LVM:
1. **Dynamic Partitioning**: LVM allows you to create, resize, and delete logical volumes without disrupting the system's operation or requiring a reboot.
2. **Improved Storage Utilization**: By pooling physical storage devices, LVM maximizes disk utilization and reduces wasted space.
3. **Volume Grouping**: Physical volumes (disks or partitions) are grouped into a "Volume Group," which acts as a container for logical volumes.
4. **Snapshot Capability**: LVM supports snapshots, which are point-in-time copies of logical volumes. Snapshots are essential for backups and data recovery.
5. **Ease of Expansion**: Logical volumes can be extended across multiple physical volumes, making storage scaling straightforward.

#### How LVM Works:
- **Physical Volumes (PVs)**: These are actual physical disks or partitions that LVM utilizes.
- **Volume Groups (VGs)**: Physical volumes are aggregated into a Volume Group, which serves as a pool of storage.
- **Logical Volumes (LVs)**: Within a Volume Group, storage is allocated to Logical Volumes, which function as independent partitions usable by the operating system.

#### Benefits of Using LVM:
- **Flexibility**: Resize or reorganize volumes without traditional partitioning limitations.
- **Scalability**: Add more storage devices and expand Volume Groups without hassle.
- **Reliability**: Snapshots and efficient management contribute to better data protection.

LVM is widely used in enterprise environments, particularly for servers and virtualized systems, due to its capability to manage storage efficiently in dynamically changing conditions.

---

### What is AppArmor?

AppArmor (Application Armor) is a robust Linux security module designed to enhance system security by enforcing mandatory access control (MAC) policies. These policies restrict applications to a predefined set of permissions, reducing the risk of unauthorized access or malicious activity.

#### Key Features of AppArmor:
1. **Policy Enforcement**: AppArmor uses profiles to define what system resources (files, directories, network access, etc.) an application can access. Profiles can be created in either *complain* or *enforce* modes.
2. **Granular Control**: Administrators can set detailed permissions, limiting applications to only what is necessary for their operation (principle of least privilege).
3. **Ease of Use**: AppArmor provides a simple, human-readable syntax for creating and editing profiles.
4. **Compatibility**: It integrates seamlessly with the Linux Security Modules (LSM) framework, making it easy to adopt in various Linux distributions.

#### How AppArmor Works:
- **Profiles**: AppArmor operates by loading profiles into the kernel that specify the access permissions for specific programs. These profiles can either:
  - **Allow**: Permit defined actions and resource usage.
  - **Deny**: Restrict or block access to certain system resources.
- **Complain Mode**: In this mode, AppArmor does not enforce restrictions but logs policy violations, making it easier to test and refine profiles.
- **Enforce Mode**: In this mode, AppArmor actively enforces the access control policies and logs any violations.

#### Benefits of Using AppArmor:
- **Enhanced Security**: By isolating applications, AppArmor minimizes the potential damage from vulnerabilities or exploits.
- **Ease of Configuration**: Profiles are easier to set up and maintain compared to other MAC frameworks like SELinux.
- **Flexibility**: Supports both predefined profiles for common applications and custom profiles tailored to specific needs.

AppArmor is widely adopted in Linux distributions such as Ubuntu and SUSE. It is particularly valued for its simplicity and efficiency in securing applications while maintaining system performance.

---

### Difference Between Apt and Aptitude

#### Apt:
Apt (Advanced Package Tool) is a lightweight, command-line package manager commonly used in Debian-based systems like Ubuntu. It is efficient and straightforward, making it ideal for quick installations, updates, and removals of packages. Apt focuses on simplicity and offers essential functionality for managing software packages.

- **Key Features**:
  - Easy to use for basic package management tasks.
  - Supports commands like `install`, `remove`, `update`, and `upgrade`.
  - Lightweight and well-suited for scripts and automated tasks.

#### Aptitude:
Aptitude is a more advanced package manager that builds upon Apt, offering additional features and a user-friendly, text-based interface. It is designed for more complex package management tasks, including better dependency resolution and conflict handling. Aptitude is particularly favored by administrators who need robust tools for maintaining large systems.

- **Key Features**:
  - Includes a text-based User Interface (TUI), simplifying navigation and package selection.
  - Superior dependency management: Aptitude can suggest solutions when package conflicts arise.
  - Provides more detailed control over package operations.

#### Key Differences:
| Feature              | Apt                        | Aptitude                   |
|----------------------|----------------------------|----------------------------|
| **Interface**        | Command-line only          | Command-line + TUI         |
| **Dependency Handling** | Basic resolution          | Advanced resolution with suggestions |
| **Use Cases**        | Simple package management  | Complex tasks and system maintenance |

Apt is ideal for users seeking a minimalistic and efficient tool, while Aptitude caters to those who need advanced features and enhanced package management capabilities.

---

### What is SSH?

SSH (Secure Shell) is a widely-used network protocol that provides a secure way to access and manage remote systems over an untrusted network. It is particularly popular in server administration, remote command execution, and file transfers. By encrypting all communication between the client and the server, SSH ensures that data remains confidential and protected from potential interception or tampering.

#### Key Features of SSH:
1. **Encryption**: All communication is encrypted, ensuring confidentiality and data integrity.
2. **Authentication**: SSH supports various authentication methods, including password-based, public key-based, and multifactor authentication, making it both flexible and secure.
3. **Port Forwarding**: SSH can tunnel traffic from other applications, allowing secure connections to services on remote systems.
4. **Secure File Transfer**: Protocols like SCP (Secure Copy Protocol) and SFTP (Secure File Transfer Protocol) operate over SSH, enabling safe file transfers.

#### How SSH Works:
- A connection begins with a **handshake** where the client and server exchange encryption keys using public-key cryptography.
- Once authenticated, the communication is encrypted using symmetric encryption, ensuring a secure session.
- During the session, all commands, data, or files exchanged between the client and server are protected from eavesdropping or man-in-the-middle attacks.

#### Benefits of SSH:
- **Enhanced Security**: Protects sensitive data, such as login credentials and commands, from exposure.
- **Remote Administration**: Allows administrators to manage systems efficiently from anywhere.
- **Flexibility**: Compatible with various devices and operating systems.

SSH is a cornerstone of secure system administration and remains a vital tool for IT professionals worldwide.

---

### What is UFW and How to Implement UFW with SSH?

#### What is UFW?
UFW (Uncomplicated Firewall) is a straightforward and user-friendly interface for managing firewall rules on Linux systems. It simplifies the process of configuring iptables, making it accessible even for users with limited experience in networking. UFW is commonly used to allow, block, or restrict access to specific services, ensuring enhanced system security.

#### Key Features of UFW:
- **Simplicity**: Designed to be easy to use with simple commands for common tasks.
- **Flexibility**: Supports both IPv4 and IPv6, allowing robust rule configurations.
- **Efficiency**: Lightweight and does not significantly impact system performance.

---

#### How to Implement UFW with SSH
When setting up UFW in systems where SSH is used for remote access, it is crucial to properly configure UFW to allow SSH connections. Here's a step-by-step guide:

**Install UFW**:
   Install UFW using the following command:
   ```bash
    sudo apt install ufw

**Allow SSH Connections**:
To avoid locking yourself out of your system, make sure to allow the SSH port through the firewall. Replace `<port>` with the actual port number your SSH service is using (default is 22).

**Run the following command**:
```bash
sudo ufw allow <port>








---
---

1️⃣ Introduction



---

What is a Virtual Machine? <a name="what-is-a-virtual-machine"></a>

A Virtual Machine (VM) is a software-based computer that runs an operating system (OS) inside another OS, using shared hardware resources (CPU, RAM, storage).

Key Properties:

➡️ Hypervisor: Software (e.g., VirtualBox, UTM) that creates/manages VMs.

➡️ Isolation: VM crashes won’t affect the host machine.

➡️ Snapshots: Save/restore VM state at any point.


Types of VMs:

➡️ Type 1 (Bare-metal): Runs directly on hardware (e.g., VMware ESXi).

➡️ Type 2 (Hosted): Runs on top of an OS (e.g., VirtualBox).


Why Use VMs?

✔ Test software safely

✔ Run multiple OSes (Linux/Windows/macOS) on one machine

✔ Clone/backup entire systems

---

How do Virtual Machines work? <a name="how-do-virtual-machines-work"></a>

Virtual Machines (VMs) operate through a hypervisor, which acts as a mediator between physical hardware and virtual environments.


▶️ Core Mechanism:

Resource Allocation: The hypervisor partitions CPU, RAM, and storage from the host machine. Each VM gets virtualized hardware (vCPU, virtual RAM, virtual disks).

Isolation: VMs run independently—a crash in one VM doesn’t affect others or the host.

Communication: The hypervisor translates VM requests into physical hardware instructions.



▶️ Key Advantages:

Efficiency: Maximizes hardware usage.

Security: Malware in a VM won’t infect the host.

Portability: VMs can be moved between physical servers.

---

What is LVM? <a name="what-is-lvm"></a>

Logical Volume Manager (LVM) is an advanced storage management system that provides flexible disk partitioning beyond traditional methods.


Core Components:

   \Physical Volume (PV): 
    
   - Actual storage devices (HDDs, SSDs, partitions)
    
   - Initialized with pvcreate /dev/sdX

   \Volume Group (VG): 
    
   - Pool of PVs that form shared storage
     
   - Created with vgcreate vg_name /dev/sdX

   \Logical Volume (LV):

   - Virtual partitions created from VG space

   - Made with lvcreate -L 10G -n lv_name vg_name


Advantages Over Traditional Partitioning:

   ✔Dynamic resizing without unmounting

   ✔Combined storage from multiple disks

   ✔Live snapshots for backups

   ✔Easy storage migration

---

What is AppArmor? <a name="what-is-apparmor"></a>

AppArmor (Application Armor) is a Linux security module that implements Mandatory Access Control (MAC) to restrict programs' capabilities through security profiles.


Key Features:

▶️Profile-based protection: Each application runs with explicitly defined permissions

▶️Two enforcement modes:

   Enforce: Actively blocks unauthorized actions

   Complain: Logs violations without blocking (learning mode)

▶️Path-based controls: Restricts access to files, network ports, and capabilities


How It Works:

   *️⃣ System administrator creates security profiles for applications

   *️⃣ AppArmor intercepts system calls and checks them against profiles

   *️⃣ Violations are either blocked or logged based on mode

---

Difference between APT and Aptitude <a name="difference-between-apt-and-aptitude"></a>

APT (Advanced Package Tool) and Aptitude are both package management tools for Debian-based systems, but with key differences:

Key Advantages of Each:

   ⏹APT:

Simpler for basic operations

Better for scripting (consistent output format)

Default on most modern Debian systems

   ⏹Aptitude:

Better at resolving complex dependency issues

Visual package browser (press ? for help)

Marks packages as automatically/manually installed

Keeps history of all package changes

---

