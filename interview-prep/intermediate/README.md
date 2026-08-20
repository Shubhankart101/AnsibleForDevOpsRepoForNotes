# Intermediate Ansible Interview Code

Focus: reusable roles, loops, handlers, validation, and rolling changes.

```yaml
- name: Configure application nodes
  hosts: app
  become: true
  serial: 2
  vars:
    app_packages: [curl, jq]
  tasks:
    - name: Install dependencies
      ansible.builtin.package:
        name: "{{ item }}"
        state: present
      loop: "{{ app_packages }}"
    - name: Render service configuration
      ansible.builtin.template:
        src: app.conf.j2
        dest: /etc/devtrack/app.conf
        mode: '0644'
      notify: Restart application
  handlers:
    - name: Restart application
      ansible.builtin.service:
        name: devtrack
        state: restarted
```

Interview checks: explain `serial`, handler de-duplication, variable precedence, and how to test a role with Molecule.
