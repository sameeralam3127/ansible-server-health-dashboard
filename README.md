# Ansible Server Performance Dashboard

## Features

- Multi-server HTML performance report
- Disk, users, OS, architecture
- Historical CPU & RAM (sysstat)
- Grafana-style dashboard
- Ansible-lint + pre-commit ready

## Requirements

- Ansible 2.14+
- Python 3
- SSH access
- sysstat supported OS

## Usage

```bash
git clone https://github.com/sameeralam3127/ansible-server-health-dashboard.git
cd ansible-server-health-dashboard
ansible-playbook playbooks/site.yml
```

Report generated in `reports/server_report.html`

---
