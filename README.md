# 🚀 Ansible Home Lab (ALP)

A minimal, ready-to-run **Ansible home lab** showcasing configuration management across Linux and Windows nodes.

For a lab overview: https://letisiapangataa.github.io/posts/home-lab-with-ansible/

## What's inside
- `ansible.cfg` — local Ansible configuration
- `inventory/` — sample inventory with `linux_servers` and `windows_servers` groups
- `playbooks/` — example playbooks:
  - `linux_hardening.yml` — UFW + SSH baseline
  - `windows_config.yml` — create a local admin user (demo)
  - `nginx.yml` — install & manage Nginx on Linux nodes
- `group_vars/all/` — global defaults (non-sensitive)
- `roles/common/` — example role structure (placeholder)
- `blog/` — Markdown blog post explaining how this lab was built

## Quick start
1. Install Ansible on your control node (Linux/macOS).
2. Update `inventory/inventory.ini` with your node IPs/hostnames.
3. Configure SSH for Linux nodes and WinRM for Windows nodes.
4. Run a playbook, e.g.:
```bash
ansible-playbook -i inventory/inventory.ini playbooks/linux_hardening.yml
```
or
```bash
ansible-playbook -i inventory/inventory.ini playbooks/nginx.yml
```

> ⚠️ **Security note:** Do **not** commit real passwords. Use Ansible Vault for secrets. The Windows example uses a placeholder that you should replace with a vaulted var.

## Using Ansible Vault (example)
Create an encrypted variable file for secrets:
```bash
ansible-vault create group_vars/all/vault.yml
```
Put secrets like:
```yaml
win_local_admin_password: "replace-with-strong-password"
```
Reference vaulted vars in your playbooks. To run with vault:
```bash
ansible-playbook -i inventory/inventory.ini playbooks/windows_config.yml --ask-vault-pass
```

## CI (optional)
A simple GitHub Actions workflow runs `ansible-lint` if available. You can remove or expand it as needed.

---

## Disclaimer

This project was developed using a combination of publicly available learning resources, reference books, open source projects, and artificial intelligence tools. All efforts have been made to attribute and comply with relevant licenses. Contributions and insights from the broader open source and educational communities are gratefully acknowledged. This software is provided as-is, without warranty of any kind, express or implied. The author assumes no responsibility for any loss, damage, or disruption caused by the use of this code. It is intended for educational and experimental purposes only and may not be suitable for production environments.
