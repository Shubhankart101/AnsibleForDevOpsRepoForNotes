# Ansible Script Library

Run examples with an inventory and start in check mode:

```bash
ansible-playbook -i inventory.ini scripts/beginner/01_ping_hosts.yml --check
```

## Levels

- `beginner/01-10`: connectivity, packages, services, users, variables, loops, facts, conditions, and handlers.
- `intermediate/11-22`: templates, validation, health checks, rolling changes, async work, delegation, and Vault.
- `advanced/23-34`: dynamic inventory, cloud modules, roles, blue-green delivery, audit, backups, certificates, and recovery.

Every file is intentionally small and focuses on one interview-ready automation pattern.
