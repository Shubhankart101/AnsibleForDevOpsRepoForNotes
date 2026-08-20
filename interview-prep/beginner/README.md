# Beginner Ansible Interview Code

Focus: inventory, idempotence, variables, handlers, and safe check mode.

Run the example with `ansible-playbook -i inventory.ini site.yml --check`.

```yaml
# site.yml
- name: Install and start a web service
  hosts: web
  become: true
  vars:
    web_package: nginx
  tasks:
    - name: Install web package
      ansible.builtin.package:
        name: "{{ web_package }}"
        state: present
    - name: Start web service
      ansible.builtin.service:
        name: "{{ web_package }}"
        state: started
        enabled: true
```

Interview checks: explain why `state: present` is idempotent, how inventory groups work, and why `--check` should precede a change.
