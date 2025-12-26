# HTU Environment Rebuild – Assignment Brief

## Introduction

Hello Trainee,

We are contacting you following a critical incident that recently affected one of our major clients, HTU. Due to the sudden departure of several members of the former SysAdmins team, large portions of the infrastructure were left without proper documentation or maintenance. This resulted in a major outage for HTU a few days ago.

HTU has expressed strong dissatisfaction and indicated that any similar incident in the future may lead to the termination of their contract, posing a serious risk to our business relationship and overall reputation.

We urgently require your support to rebuild and stabilize HTU’s environment from the ground up. As they operate an Enterprise Multi-User Environment, the system must be reconstructed with proper security, user access control, storage integrity, and service reliability.

Because no documentation was left behind, you must perform a complete reinstallation and reconfiguration of their RHEL server from scratch.

---

## 1. Server Rebuild Task

- 4 vCPU
- 4 GB RAM
- 20 GB Disk
- 40 GB Disk
- Operating System: Red Hat Enterprise Linux (RHEL)

---

## 2. OS Installation Requirements

### 2.1 Language & Localization
- Language: English (US)
- Keyboard: English (US)
- Timezone: Asia/Amman

### 2.2 Disk & Partitioning
- Select the 20 GB disk
- Use Automatic Partitioning

### 2.3 User Configuration
- Disable direct root login
- Create administrative user:
  - Username: sysadmin
  - Add to wheel group
  - Strong password

### 2.4 Software Selection
- Minimal Install
- Default settings

### 2.5 Automated Installation (Kickstart)
- Fully automated
- Reflects all installation settings
- Used for repeatable deployments

---

## 3. Initial System Setup (Post-Installation)

- Register server with Red Hat Subscription Management
- Enable official repositories
- Update all packages
- Install: nano, VDO, kmod-kvdo, rsync, tuned, httpd/nginx, net-tools

---

## 4. Storage Configuration (40GB Disk)

- GPT partition table
- Single LVM partition
- XFS filesystem

Logical Volumes:
- /home (15GB) migrated, original renamed to /home.bak
- /company (10GB)
- Additional swap (RAM-based)

Persistence via /etc/fstab

---

## 5. Departmental Directory Structure

- /company/hr
- /company/finance
- /company/engineering
- /company/management

Permissions:
- Department isolation
- Group collaboration
- Inherit group ownership
- Prevent deletion of others’ files

---

## 6. User Groups and Accounts

Groups:
hr, finance, engineering, management, it

Users:
sara, huda, ahmed, rami, omar, ali, manager, admin1, admin2

Password for all users: Htu@123

Only IT users have administrative privileges.

---

## 7. Backup Mechanism

- Archive all /company directories daily
- Compress to .tar
- Store in /backup
- Cron job runs at 11:59 AM

---

## 8. Server Optimization with TuneD

- Install TuneD
- Enable at boot
- Apply virtual-guest profile

---

## 9. System Identity

Hostname:
htu-server.ceu.local

Ensure local hostname resolution without DNS.

---

## 10. YUM Repository Configuration

BaseOS:
http://content.example.com/rhel8.0/x86_64/dvd/BaseOS

AppStream:
http://content.example.com/rhel8.0/x86_64/dvd/AppStream

---

## 11. Temporary HR Web Application Placeholder

- Directory: /opt/hr_placeholder
- Simple “Coming Soon” page
- Apache or Nginx
- Port 82
- systemd managed
- SELinux enforcing
- Firewall allows port 82

---

## 12. SSH Service Hardening

- SSH key authentication for sysadmin
- Disable password authentication
- Restrict SSH access to administrative users only
