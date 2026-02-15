# Ansible Server Health Dashboard

A role-based Ansible project that collects Linux server metrics (CPU, RAM, Disk usage) and generates a centralized HTML dashboard report.

## Features

- Collects:
  - CPU cores
  - Memory usage
  - Disk usage (root partition)
  - OS details
  - IP address
- Generates consolidated HTML report
- Color-coded health indicators
- Role-prefixed variables (lint compliant)
- Explicit file permissions (security-safe)
- Pre-commit enforced quality checks

---

## Requirements

- Python 3.10+
- Ansible Core 2.16+
- ansible-lint v26+
- pre-commit

Install dependencies:

```bash
pip install ansible-core ansible-lint pre-commit
```

---

## Usage

### Configure Inventory

Edit:

```
inventory/hosts.ini
```

Example:

```ini
[linux_servers]
server1 ansible_host=192.168.1.10
server2 ansible_host=192.168.1.11

[linux_servers:vars]
ansible_user=ubuntu
ansible_become=true
```

---

### Run Playbook

```bash
ansible-playbook -i inventory/hosts.ini site.yml
```

---

### View Report

Open:

```
reports/system_report.html
```

---

## Dashboard Output

The generated dashboard includes:

- Memory usage percentage
- Disk usage percentage
- Health coloring:
  - 🟢 OK (< 60%)
  - 🟠 Warning (60–80%)
  - 🔴 Critical (> 80%)

---

## Code Quality (Pre-commit)

This project enforces:

- ansible-lint rules
- YAML validation
- trailing whitespace removal
- end-of-file fixes

### Install hooks

```bash
pre-commit install
```

### Run manually

```bash
pre-commit run --all-files
```

---

## Lint Compliance

The role follows:

- Role-prefixed variables
- Explicit file permissions
- Proper task naming conventions
- Modern `ansible_facts` usage
- Safe Jinja formatting

---

## License

MIT License
