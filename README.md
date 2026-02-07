# Ansible Server Performance Report

**One-command Ansible playbook that collects Linux server performance data and generates a beautiful HTML report.**

No Prometheus, no Grafana, no agents needed to run permanently — just run the playbook when you want a snapshot of your server's health.

Perfect for:

- Quick health checks on personal servers, VPS, homelabs
- Weekly/monthly reports for small teams
- Troubleshooting performance issues
- Getting visibility without installing heavy monitoring stacks

## What this playbook collects

- CPU usage (load average, per-core usage, iowait, steal, etc.)
- Memory usage (total, used, free, cached, swap)
- Disk usage & I/O (space used, inodes, read/write stats)
- Top processes by CPU and memory
- Logged-in users & who is doing what
- System information (kernel, uptime, distribution, hostname)
- Basic network interfaces status
- (Optional) sar/sysstat historical data if sysstat is installed

The result is a **single self-contained HTML report** with tables, progress bars, and color coding.

## Features

- Works on **most modern Linux distributions**
- Very few dependencies
- Generates nice-looking HTML report (no external CSS/CDN required)
- Easy to customize — add your own checks or change the look
- Supports multiple servers at once (inventory based)
- Idempotent & safe to run repeatedly

## Supported Distributions

| Distribution         | Support level | Notes                          |
| -------------------- | ------------- | ------------------------------ |
| Ubuntu 20.04 / 22.04 | Excellent     | Fully tested                   |
| Debian 11 / 12       | Excellent     | Fully tested                   |
| CentOS Stream 8 / 9  | Good          | Works well                     |
| Rocky Linux 8 / 9    | Good          | Works well                     |
| AlmaLinux 8 / 9      | Good          | Works well                     |
| Fedora 39+           | Good          | Should work                    |
| RHEL 8 / 9           | Good          | Should work (EPEL for sysstat) |

## Prerequisites

On your **control machine** (where you run ansible):

- Ansible ≥ 2.14 (recommended: latest version)
- Python 3

On the **target servers**:

- Python 3 (usually already installed)
- `sudo` privileges for the ansible user (become: yes)
- (Optional but recommended) `sysstat` package installed for better historical data

## Quick Start (3 minutes)

### 1. Clone the project

```bash
git clone https://github.com/sameeralam3127/ansible-server-health-dashboard.git
cd ansible-server-health-dashboard
```

### 2. Install requirements (if any)

```bash
ansible-galaxy install -r requirements.yml
```

(If the file is empty right now — you can skip this step)

### 3. Edit the inventory

Open `inventory/hosts.ini` and add your servers:

```ini
[linux_servers]
server1.example.com  ansible_host=192.168.1.101  ansible_user=youruser
server2.example.com  ansible_host=10.20.30.40    ansible_user=admin
web01.mycompany.local
db02.mycompany.local ansible_ssh_private_key_file=~/.ssh/id_rsa_prod
```

### 5. Run the playbook

```bash
ansible-playbook -i inventory/hosts.ini playbooks/site.yml
```

Or with extra verbosity (recommended first time):

```bash
ansible-playbook -i inventory/hosts.ini playbooks/site.yml -v
```

### 6. Find your report

After the run finishes, look in the `reports/` folder:

```
reports/
└── server_report_2025-02-08_ubuntu-server1.html
```

Just open the file in any browser.

## Common Usage Examples

Run on one host only:

```bash
ansible-playbook -i inventory/hosts.ini playbooks/site.yml --limit server1.example.com
```

Run with password prompt (if no key-based auth):

```bash
ansible-playbook -i inventory/hosts.ini playbooks/site.yml --ask-become-pass
```

Run and save reports to custom location:

```bash
ansible-playbook -i inventory/hosts.ini playbooks/site.yml -e "report_output_dir=/home/user/monthly-reports"
```
