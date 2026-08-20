# Advanced Ansible Interview Code

Focus: controlled rollout, failure recovery, vault boundaries, and observable automation.

```yaml
- name: Deploy with health-gated rollback
  hosts: app
  serial: 1
  max_fail_percentage: 0
  tasks:
    - name: Deploy release
      block:
        - ansible.builtin.unarchive:
            src: "releases/{{ release_id }}.tar.gz"
            dest: /opt/devtrack/releases/{{ release_id }}
        - ansible.builtin.uri:
            url: http://127.0.0.1:8080/health
            status_code: 200
      rescue:
        - name: Restore previous release
          ansible.builtin.command:
            cmd: /opt/devtrack/bin/rollback
          changed_when: true
      always:
        - name: Emit deployment result
          ansible.builtin.debug:
            msg: "release={{ release_id }} host={{ inventory_hostname }}"
```

Interview checks: explain failure domains, `block/rescue/always`, secret handling with Ansible Vault, and how you would make the rollback command safe.
