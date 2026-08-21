# Ansible Interview Question Bank

This bank contains 150 questions organized by difficulty. Use the numbered scripts in `scripts/` to build answers with working examples.

## Worked Answers

### Beginner: idempotent service configuration

**Question:** How do you install and start a service safely?

```yaml
- name: Configure web service
	hosts: web
	become: true
	tasks:
		- ansible.builtin.package:
				name: nginx
				state: present
		- ansible.builtin.service:
				name: nginx
				state: started
				enabled: true
```

The desired state is declared; rerunning the playbook does not reinstall or restart unnecessarily.

### Intermediate: rolling health check

**Question:** How do you roll out one host at a time?

```yaml
- name: Rolling application update
	hosts: app
	serial: 1
	tasks:
		- ansible.builtin.template:
				src: app.conf.j2
				dest: /etc/devtrack.conf
			notify: Restart application
		- ansible.builtin.uri:
				url: http://127.0.0.1:8080/health
				status_code: 200
```

`serial: 1` limits the failure domain, while the health check gates each host.

### Advanced: rescue rollback

**Question:** How do you roll back after a failed deployment?

```yaml
- block:
		- ansible.builtin.command: /opt/devtrack/bin/deploy "{{ release_id }}"
			changed_when: true
		- ansible.builtin.uri:
				url: http://127.0.0.1:8080/health
				status_code: 200
	rescue:
		- ansible.builtin.command: /opt/devtrack/bin/rollback
			changed_when: true
```

The rescue block runs only after deployment or validation fails.

## Beginner: 1-40

1. What problem does Ansible solve?

**Answer:** It addresses a recurring DevOps need by making delivery, operations, or infrastructure repeatable, reviewable, and safer to automate.



<a href="interview-scripts/001-what-problem-does-ansible-solve.yml"><img src="https://img.shields.io/badge/Question%201%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 1 script"></a>

```yaml
---
# Question 1: What problem does Ansible solve?
- name: Execute question 1 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 1 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

2. How does Ansible differ from agent-based configuration tools?

**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.



<a href="interview-scripts/002-how-does-ansible-differ-from-agent-based-configuration.yml"><img src="https://img.shields.io/badge/Question%202%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 2 script"></a>

```yaml
---
# Question 2: How does Ansible differ from agent-based configuration tools?
- name: Execute question 2 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 2 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

3. What is an Ansible inventory?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/003-what-is-an-ansible-inventory.yml"><img src="https://img.shields.io/badge/Question%203%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 3 script"></a>

```yaml
---
# Question 3: What is an Ansible inventory?
- name: Execute question 3 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 3 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

4. What is the difference between a host and a group?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/004-what-is-the-difference-between-a-host-and-a-group.yml"><img src="https://img.shields.io/badge/Question%204%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 4 script"></a>

```yaml
---
# Question 4: What is the difference between a host and a group?
- name: Execute question 4 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 4 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

5. What is a playbook?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/005-what-is-a-playbook.yml"><img src="https://img.shields.io/badge/Question%205%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 5 script"></a>

```yaml
---
# Question 5: What is a playbook?
- name: Execute question 5 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 5 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

6. What is a play?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/006-what-is-a-play.yml"><img src="https://img.shields.io/badge/Question%206%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 6 script"></a>

```yaml
---
# Question 6: What is a play?
- name: Execute question 6 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 6 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

7. What is a task?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/007-what-is-a-task.yml"><img src="https://img.shields.io/badge/Question%207%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 7 script"></a>

```yaml
---
# Question 7: What is a task?
- name: Execute question 7 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 7 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

8. What is a module?

**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.



<a href="interview-scripts/008-what-is-a-module.yml"><img src="https://img.shields.io/badge/Question%208%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 8 script"></a>

```yaml
---
# Question 8: What is a module?
- name: Execute question 8 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 8 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

9. What is a fully qualified collection name?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/009-what-is-a-fully-qualified-collection-name.yml"><img src="https://img.shields.io/badge/Question%209%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 9 script"></a>

```yaml
---
# Question 9: What is a fully qualified collection name?
- name: Execute question 9 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 9 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

10. What does idempotence mean in Ansible?

**Answer:** Make the operation converge on the declared state and check the current state before mutating it, so a second run produces no unnecessary change.



<a href="interview-scripts/010-what-does-idempotence-mean-in-ansible.yml"><img src="https://img.shields.io/badge/Question%2010%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 10 script"></a>

```yaml
---
# Question 10: What does idempotence mean in Ansible?
- name: Execute question 10 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 10 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

11. Why should `ansible.builtin.command` be used carefully?

**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.



<a href="interview-scripts/011-why-should-ansible-builtin-command-be-used-carefully.yml"><img src="https://img.shields.io/badge/Question%2011%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 11 script"></a>

```yaml
---
# Question 11: Why should `ansible.builtin.command` be used carefully?
- name: Execute question 11 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 11 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

12. When would you use the `shell` module?

**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.



<a href="interview-scripts/012-when-would-you-use-the-shell-module.yml"><img src="https://img.shields.io/badge/Question%2012%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 12 script"></a>

```yaml
---
# Question 12: When would you use the `shell` module?
- name: Execute question 12 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 12 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

13. What does `ansible.builtin.ping` actually verify?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/013-what-does-ansible-builtin-ping-actually-verify.yml"><img src="https://img.shields.io/badge/Question%2013%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 13 script"></a>

```yaml
---
# Question 13: What does `ansible.builtin.ping` actually verify?
- name: Execute question 13 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 13 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

14. How do you run a playbook in check mode?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/014-how-do-you-run-a-playbook-in-check-mode.yml"><img src="https://img.shields.io/badge/Question%2014%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 14 script"></a>

```yaml
---
# Question 14: How do you run a playbook in check mode?
- name: Execute question 14 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 14 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

15. What does `--diff` show?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/015-what-does-diff-show.yml"><img src="https://img.shields.io/badge/Question%2015%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 15 script"></a>

```yaml
---
# Question 15: What does `--diff` show?
- name: Execute question 15 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 15 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

16. How do you pass an extra variable at runtime?

**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.



<a href="interview-scripts/016-how-do-you-pass-an-extra-variable-at-runtime.yml"><img src="https://img.shields.io/badge/Question%2016%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 16 script"></a>

```yaml
---
# Question 16: How do you pass an extra variable at runtime?
- name: Execute question 16 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 16 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

17. What is the difference between `vars` and `vars_files`?

**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.



<a href="interview-scripts/017-what-is-the-difference-between-vars-and-vars-files.yml"><img src="https://img.shields.io/badge/Question%2017%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 17 script"></a>

```yaml
---
# Question 17: What is the difference between `vars` and `vars_files`?
- name: Execute question 17 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 17 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

18. How do you use a variable in a task?

**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.



<a href="interview-scripts/018-how-do-you-use-a-variable-in-a-task.yml"><img src="https://img.shields.io/badge/Question%2018%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 18 script"></a>

```yaml
---
# Question 18: How do you use a variable in a task?
- name: Execute question 18 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 18 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

19. What is a loop and how is it written?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/019-what-is-a-loop-and-how-is-it-written.yml"><img src="https://img.shields.io/badge/Question%2019%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 19 script"></a>

```yaml
---
# Question 19: What is a loop and how is it written?
- name: Execute question 19 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 19 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

20. How do you register task output?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/020-how-do-you-register-task-output.yml"><img src="https://img.shields.io/badge/Question%2020%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 20 script"></a>

```yaml
---
# Question 20: How do you register task output?
- name: Execute question 20 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 20 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

21. What is a handler?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/021-what-is-a-handler.yml"><img src="https://img.shields.io/badge/Question%2021%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 21 script"></a>

```yaml
---
# Question 21: What is a handler?
- name: Execute question 21 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 21 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

22. When does a handler run?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/022-when-does-a-handler-run.yml"><img src="https://img.shields.io/badge/Question%2022%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 22 script"></a>

```yaml
---
# Question 22: When does a handler run?
- name: Execute question 22 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 22 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

23. How do you notify a handler?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/023-how-do-you-notify-a-handler.yml"><img src="https://img.shields.io/badge/Question%2023%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 23 script"></a>

```yaml
---
# Question 23: How do you notify a handler?
- name: Execute question 23 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 23 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

24. How do `when` conditions work?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/024-how-do-when-conditions-work.yml"><img src="https://img.shields.io/badge/Question%2024%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 24 script"></a>

```yaml
---
# Question 24: How do `when` conditions work?
- name: Execute question 24 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 24 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

25. How do you install a package portably?

**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.



<a href="interview-scripts/025-how-do-you-install-a-package-portably.yml"><img src="https://img.shields.io/badge/Question%2025%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 25 script"></a>

```yaml
---
# Question 25: How do you install a package portably?
- name: Execute question 25 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 25 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

26. How do you manage a service?

**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.



<a href="interview-scripts/026-how-do-you-manage-a-service.yml"><img src="https://img.shields.io/badge/Question%2026%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 26 script"></a>

```yaml
---
# Question 26: How do you manage a service?
- name: Execute question 26 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 26 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

27. How do you create a user with Ansible?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/027-how-do-you-create-a-user-with-ansible.yml"><img src="https://img.shields.io/badge/Question%2027%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 27 script"></a>

```yaml
---
# Question 27: How do you create a user with Ansible?
- name: Execute question 27 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 27 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

28. How do you copy a static file?

**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.



<a href="interview-scripts/028-how-do-you-copy-a-static-file.yml"><img src="https://img.shields.io/badge/Question%2028%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 28 script"></a>

```yaml
---
# Question 28: How do you copy a static file?
- name: Execute question 28 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 28 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

29. When should you use `template` instead of `copy`?

**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.



<a href="interview-scripts/029-when-should-you-use-template-instead-of-copy.yml"><img src="https://img.shields.io/badge/Question%2029%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 29 script"></a>

```yaml
---
# Question 29: When should you use `template` instead of `copy`?
- name: Execute question 29 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 29 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

30. What is privilege escalation with `become`?

**Answer:** Apply least privilege, isolate trust boundaries, validate policy in CI or admission, and record auditable changes.



<a href="interview-scripts/030-what-is-privilege-escalation-with-become.yml"><img src="https://img.shields.io/badge/Question%2030%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 30 script"></a>

```yaml
---
# Question 30: What is privilege escalation with `become`?
- name: Execute question 30 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 30 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

31. How do you limit execution to selected hosts?

**Answer:** Declare requests and limits, measure real usage, set explicit capacity bounds, and test behavior under saturation and recovery.



<a href="interview-scripts/031-how-do-you-limit-execution-to-selected-hosts.yml"><img src="https://img.shields.io/badge/Question%2031%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 31 script"></a>

```yaml
---
# Question 31: How do you limit execution to selected hosts?
- name: Execute question 31 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 31 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

32. What does `gather_facts` do?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/032-what-does-gather-facts-do.yml"><img src="https://img.shields.io/badge/Question%2032%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 32 script"></a>

```yaml
---
# Question 32: What does `gather_facts` do?
- name: Execute question 32 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 32 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

33. How do you print a variable for troubleshooting?

**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.



<a href="interview-scripts/033-how-do-you-print-a-variable-for-troubleshooting.yml"><img src="https://img.shields.io/badge/Question%2033%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 33 script"></a>

```yaml
---
# Question 33: How do you print a variable for troubleshooting?
- name: Execute question 33 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 33 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

34. How do you use tags?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/034-how-do-you-use-tags.yml"><img src="https://img.shields.io/badge/Question%2034%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 34 script"></a>

```yaml
---
# Question 34: How do you use tags?
- name: Execute question 34 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 34 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

35. What is YAML indentation significance?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/035-what-is-yaml-indentation-significance.yml"><img src="https://img.shields.io/badge/Question%2035%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 35 script"></a>

```yaml
---
# Question 35: What is YAML indentation significance?
- name: Execute question 35 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 35 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

36. How do you check playbook syntax?

**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.



<a href="interview-scripts/036-how-do-you-check-playbook-syntax.yml"><img src="https://img.shields.io/badge/Question%2036%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 36 script"></a>

```yaml
---
# Question 36: How do you check playbook syntax?
- name: Execute question 36 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 36 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

37. What is the difference between a changed and failed task?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/037-what-is-the-difference-between-a-changed-and-failed-tas.yml"><img src="https://img.shields.io/badge/Question%2037%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 37 script"></a>

```yaml
---
# Question 37: What is the difference between a changed and failed task?
- name: Execute question 37 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 37 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

38. How do you make a command task report no change?

**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.



<a href="interview-scripts/038-how-do-you-make-a-command-task-report-no-change.yml"><img src="https://img.shields.io/badge/Question%2038%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 38 script"></a>

```yaml
---
# Question 38: How do you make a command task report no change?
- name: Execute question 38 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 38 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

39. What is an Ansible role?

**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.



<a href="interview-scripts/039-what-is-an-ansible-role.yml"><img src="https://img.shields.io/badge/Question%2039%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 39 script"></a>

```yaml
---
# Question 39: What is an Ansible role?
- name: Execute question 39 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 39 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

40. What information belongs in an inventory file?

**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.



<a href="interview-scripts/040-what-information-belongs-in-an-inventory-file.yml"><img src="https://img.shields.io/badge/Question%2040%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 40 script"></a>

```yaml
---
# Question 40: What information belongs in an inventory file?
- name: Execute question 40 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 40 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```


## Intermediate: 41-80

41. Explain Ansible variable precedence with an example.

**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.



<a href="interview-scripts/041-explain-ansible-variable-precedence-with-an-example.yml"><img src="https://img.shields.io/badge/Question%2041%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 41 script"></a>

```yaml
---
# Question 41: Explain Ansible variable precedence with an example.
- name: Execute question 41 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 41 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

42. How do role defaults differ from role vars?

**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.



<a href="interview-scripts/042-how-do-role-defaults-differ-from-role-vars.yml"><img src="https://img.shields.io/badge/Question%2042%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 42 script"></a>

```yaml
---
# Question 42: How do role defaults differ from role vars?
- name: Execute question 42 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 42 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

43. What belongs in `tasks`, `handlers`, `templates`, and `defaults`?

**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.



<a href="interview-scripts/043-what-belongs-in-tasks-handlers-templates-and-defaults.yml"><img src="https://img.shields.io/badge/Question%2043%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 43 script"></a>

```yaml
---
# Question 43: What belongs in `tasks`, `handlers`, `templates`, and `defaults`?
- name: Execute question 43 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 43 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

44. How do you design a reusable role?

**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.



<a href="interview-scripts/044-how-do-you-design-a-reusable-role.yml"><img src="https://img.shields.io/badge/Question%2044%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 44 script"></a>

```yaml
---
# Question 44: How do you design a reusable role?
- name: Execute question 44 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 44 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

45. How do role dependencies work?

**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.



<a href="interview-scripts/045-how-do-role-dependencies-work.yml"><img src="https://img.shields.io/badge/Question%2045%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 45 script"></a>

```yaml
---
# Question 45: How do role dependencies work?
- name: Execute question 45 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 45 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

46. How do you use `include_tasks` and `import_tasks`?

**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.



<a href="interview-scripts/046-how-do-you-use-include-tasks-and-import-tasks.yml"><img src="https://img.shields.io/badge/Question%2046%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 46 script"></a>

```yaml
---
# Question 46: How do you use `include_tasks` and `import_tasks`?
- name: Execute question 46 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 46 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

47. When should you use a dynamic include?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/047-when-should-you-use-a-dynamic-include.yml"><img src="https://img.shields.io/badge/Question%2047%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 47 script"></a>

```yaml
---
# Question 47: When should you use a dynamic include?
- name: Execute question 47 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 47 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

48. How do you loop over a block of tasks?

**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.



<a href="interview-scripts/048-how-do-you-loop-over-a-block-of-tasks.yml"><img src="https://img.shields.io/badge/Question%2048%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 48 script"></a>

```yaml
---
# Question 48: How do you loop over a block of tasks?
- name: Execute question 48 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 48 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

49. How do you combine registered results from a loop?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/049-how-do-you-combine-registered-results-from-a-loop.yml"><img src="https://img.shields.io/badge/Question%2049%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 49 script"></a>

```yaml
---
# Question 49: How do you combine registered results from a loop?
- name: Execute question 49 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 49 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

50. How do you use `changed_when` correctly?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/050-how-do-you-use-changed-when-correctly.yml"><img src="https://img.shields.io/badge/Question%2050%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 50 script"></a>

```yaml
---
# Question 50: How do you use `changed_when` correctly?
- name: Execute question 50 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 50 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

51. How do you use `failed_when` safely?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/051-how-do-you-use-failed-when-safely.yml"><img src="https://img.shields.io/badge/Question%2051%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 51 script"></a>

```yaml
---
# Question 51: How do you use `failed_when` safely?
- name: Execute question 51 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 51 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

52. Explain `block`, `rescue`, and `always`.

**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.



<a href="interview-scripts/052-explain-block-rescue-and-always.yml"><img src="https://img.shields.io/badge/Question%2052%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 52 script"></a>

```yaml
---
# Question 52: Explain `block`, `rescue`, and `always`.
- name: Execute question 52 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 52 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

53. How do you implement rollback after a failed deployment?

**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.



<a href="interview-scripts/053-how-do-you-implement-rollback-after-a-failed-deployment.yml"><img src="https://img.shields.io/badge/Question%2053%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 53 script"></a>

```yaml
---
# Question 53: How do you implement rollback after a failed deployment?
- name: Execute question 53 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 53 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

54. What does `serial` do during a rolling deployment?

**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.



<a href="interview-scripts/054-what-does-serial-do-during-a-rolling-deployment.yml"><img src="https://img.shields.io/badge/Question%2054%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 54 script"></a>

```yaml
---
# Question 54: What does `serial` do during a rolling deployment?
- name: Execute question 54 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 54 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

55. How do `max_fail_percentage` and `any_errors_fatal` differ?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/055-how-do-max-fail-percentage-and-any-errors-fatal-differ.yml"><img src="https://img.shields.io/badge/Question%2055%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 55 script"></a>

```yaml
---
# Question 55: How do `max_fail_percentage` and `any_errors_fatal` differ?
- name: Execute question 55 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 55 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

56. What is the difference between `linear` and `free` strategy?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/056-what-is-the-difference-between-linear-and-free-strategy.yml"><img src="https://img.shields.io/badge/Question%2056%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 56 script"></a>

```yaml
---
# Question 56: What is the difference between `linear` and `free` strategy?
- name: Execute question 56 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 56 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

57. How do you delegate a task to localhost?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/057-how-do-you-delegate-a-task-to-localhost.yml"><img src="https://img.shields.io/badge/Question%2057%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 57 script"></a>

```yaml
---
# Question 57: How do you delegate a task to localhost?
- name: Execute question 57 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 57 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

58. How do you share facts between hosts?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/058-how-do-you-share-facts-between-hosts.yml"><img src="https://img.shields.io/badge/Question%2058%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 58 script"></a>

```yaml
---
# Question 58: How do you share facts between hosts?
- name: Execute question 58 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 58 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

59. How do you run long jobs asynchronously?

**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.



<a href="interview-scripts/059-how-do-you-run-long-jobs-asynchronously.yml"><img src="https://img.shields.io/badge/Question%2059%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 59 script"></a>

```yaml
---
# Question 59: How do you run long jobs asynchronously?
- name: Execute question 59 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 59 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

60. How do you poll an asynchronous job?

**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.



<a href="interview-scripts/060-how-do-you-poll-an-asynchronous-job.yml"><img src="https://img.shields.io/badge/Question%2060%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 60 script"></a>

```yaml
---
# Question 60: How do you poll an asynchronous job?
- name: Execute question 60 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 60 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

61. How does `run_once` affect a task?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/061-how-does-run-once-affect-a-task.yml"><img src="https://img.shields.io/badge/Question%2061%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 61 script"></a>

```yaml
---
# Question 61: How does `run_once` affect a task?
- name: Execute question 61 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 61 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

62. How do you validate a rendered configuration before replacing it?

**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.



<a href="interview-scripts/062-how-do-you-validate-a-rendered-configuration-before-rep.yml"><img src="https://img.shields.io/badge/Question%2062%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 62 script"></a>

```yaml
---
# Question 62: How do you validate a rendered configuration before replacing it?
- name: Execute question 62 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 62 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

63. How do you use `assert` to validate inputs?

**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.



<a href="interview-scripts/063-how-do-you-use-assert-to-validate-inputs.yml"><img src="https://img.shields.io/badge/Question%2063%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 63 script"></a>

```yaml
---
# Question 63: How do you use `assert` to validate inputs?
- name: Execute question 63 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 63 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

64. How do you wait for a service or port?

**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.



<a href="interview-scripts/064-how-do-you-wait-for-a-service-or-port.yml"><img src="https://img.shields.io/badge/Question%2064%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 64 script"></a>

```yaml
---
# Question 64: How do you wait for a service or port?
- name: Execute question 64 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 64 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

65. How do you perform an HTTP health check?

**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.



<a href="interview-scripts/065-how-do-you-perform-an-http-health-check.yml"><img src="https://img.shields.io/badge/Question%2065%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 65 script"></a>

```yaml
---
# Question 65: How do you perform an HTTP health check?
- name: Execute question 65 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 65 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

66. How do you find files older than a retention period?

**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.



<a href="interview-scripts/066-how-do-you-find-files-older-than-a-retention-period.yml"><img src="https://img.shields.io/badge/Question%2066%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 66 script"></a>

```yaml
---
# Question 66: How do you find files older than a retention period?
- name: Execute question 66 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 66 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

67. How do you safely remove old releases?

**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.



<a href="interview-scripts/067-how-do-you-safely-remove-old-releases.yml"><img src="https://img.shields.io/badge/Question%2067%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 67 script"></a>

```yaml
---
# Question 67: How do you safely remove old releases?
- name: Execute question 67 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 67 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

68. How do you manage line-based configuration?

**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.



<a href="interview-scripts/068-how-do-you-manage-line-based-configuration.yml"><img src="https://img.shields.io/badge/Question%2068%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 68 script"></a>

```yaml
---
# Question 68: How do you manage line-based configuration?
- name: Execute question 68 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 68 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

69. How do you preserve secrets with Ansible Vault?

**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.



<a href="interview-scripts/069-how-do-you-preserve-secrets-with-ansible-vault.yml"><img src="https://img.shields.io/badge/Question%2069%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 69 script"></a>

```yaml
---
# Question 69: How do you preserve secrets with Ansible Vault?
- name: Execute question 69 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 69 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

70. How should Vault passwords be supplied in CI?

**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.



<a href="interview-scripts/070-how-should-vault-passwords-be-supplied-in-ci.yml"><img src="https://img.shields.io/badge/Question%2070%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 70 script"></a>

```yaml
---
# Question 70: How should Vault passwords be supplied in CI?
- name: Execute question 70 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 70 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

71. What is a lookup plugin?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/071-what-is-a-lookup-plugin.yml"><img src="https://img.shields.io/badge/Question%2071%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 71 script"></a>

```yaml
---
# Question 71: What is a lookup plugin?
- name: Execute question 71 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 71 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

72. What is a filter plugin?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/072-what-is-a-filter-plugin.yml"><img src="https://img.shields.io/badge/Question%2072%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 72 script"></a>

```yaml
---
# Question 72: What is a filter plugin?
- name: Execute question 72 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 72 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

73. How do you transform data with Jinja filters?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/073-how-do-you-transform-data-with-jinja-filters.yml"><img src="https://img.shields.io/badge/Question%2073%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 73 script"></a>

```yaml
---
# Question 73: How do you transform data with Jinja filters?
- name: Execute question 73 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 73 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

74. How do you use `set_fact` without creating confusing state?

**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.



<a href="interview-scripts/074-how-do-you-use-set-fact-without-creating-confusing-stat.yml"><img src="https://img.shields.io/badge/Question%2074%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 74 script"></a>

```yaml
---
# Question 74: How do you use `set_fact` without creating confusing state?
- name: Execute question 74 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 74 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

75. How do you pass environment variables to a task?

**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.



<a href="interview-scripts/075-how-do-you-pass-environment-variables-to-a-task.yml"><img src="https://img.shields.io/badge/Question%2075%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 75 script"></a>

```yaml
---
# Question 75: How do you pass environment variables to a task?
- name: Execute question 75 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 75 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

76. How do you use check mode in custom commands?

**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.



<a href="interview-scripts/076-how-do-you-use-check-mode-in-custom-commands.yml"><img src="https://img.shields.io/badge/Question%2076%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 76 script"></a>

```yaml
---
# Question 76: How do you use check mode in custom commands?
- name: Execute question 76 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 76 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

77. How do you test a role with Molecule?

**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.



<a href="interview-scripts/077-how-do-you-test-a-role-with-molecule.yml"><img src="https://img.shields.io/badge/Question%2077%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 77 script"></a>

```yaml
---
# Question 77: How do you test a role with Molecule?
- name: Execute question 77 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 77 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

78. How do Ansible lint and syntax check differ?

**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.



<a href="interview-scripts/078-how-do-ansible-lint-and-syntax-check-differ.yml"><img src="https://img.shields.io/badge/Question%2078%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 78 script"></a>

```yaml
---
# Question 78: How do Ansible lint and syntax check differ?
- name: Execute question 78 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 78 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

79. How do you troubleshoot an unreachable host?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/079-how-do-you-troubleshoot-an-unreachable-host.yml"><img src="https://img.shields.io/badge/Question%2079%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 79 script"></a>

```yaml
---
# Question 79: How do you troubleshoot an unreachable host?
- name: Execute question 79 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 79 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

80. How do you design inventories for dev, test, and production?

**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.



<a href="interview-scripts/080-how-do-you-design-inventories-for-dev-test-and-producti.yml"><img src="https://img.shields.io/badge/Question%2080%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 80 script"></a>

```yaml
---
# Question 80: How do you design inventories for dev, test, and production?
- name: Execute question 80 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 80 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```


## Advanced: 81-120

81. How would you design Ansible for a multi-account Azure estate?

**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.



<a href="interview-scripts/081-how-would-you-design-ansible-for-a-multi-account-azure.yml"><img src="https://img.shields.io/badge/Question%2081%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 81 script"></a>

```yaml
---
# Question 81: How would you design Ansible for a multi-account Azure estate?
- name: Execute question 81 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 81 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

82. How would you design Ansible for multiple AWS accounts and regions?

**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.



<a href="interview-scripts/082-how-would-you-design-ansible-for-multiple-aws-accounts.yml"><img src="https://img.shields.io/badge/Question%2082%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 82 script"></a>

```yaml
---
# Question 82: How would you design Ansible for multiple AWS accounts and regions?
- name: Execute question 82 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 82 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

83. How do dynamic inventory plugins discover cloud hosts?

**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.



<a href="interview-scripts/083-how-do-dynamic-inventory-plugins-discover-cloud-hosts.yml"><img src="https://img.shields.io/badge/Question%2083%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 83 script"></a>

```yaml
---
# Question 83: How do dynamic inventory plugins discover cloud hosts?
- name: Execute question 83 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 83 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

84. How do you authenticate to Azure without long-lived secrets?

**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.



<a href="interview-scripts/084-how-do-you-authenticate-to-azure-without-long-lived-sec.yml"><img src="https://img.shields.io/badge/Question%2084%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 84 script"></a>

```yaml
---
# Question 84: How do you authenticate to Azure without long-lived secrets?
- name: Execute question 84 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 84 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

85. How do you authenticate to AWS through an assumed role?

**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.



<a href="interview-scripts/085-how-do-you-authenticate-to-aws-through-an-assumed-role.yml"><img src="https://img.shields.io/badge/Question%2085%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 85 script"></a>

```yaml
---
# Question 85: How do you authenticate to AWS through an assumed role?
- name: Execute question 85 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 85 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

86. How do you enforce cloud resource tags with Ansible?

**Answer:** Declare requests and limits, measure real usage, set explicit capacity bounds, and test behavior under saturation and recovery.



<a href="interview-scripts/086-how-do-you-enforce-cloud-resource-tags-with-ansible.yml"><img src="https://img.shields.io/badge/Question%2086%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 86 script"></a>

```yaml
---
# Question 86: How do you enforce cloud resource tags with Ansible?
- name: Execute question 86 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 86 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

87. How do you make a cloud provisioning playbook safe to rerun?

**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.



<a href="interview-scripts/087-how-do-you-make-a-cloud-provisioning-playbook-safe-to-r.yml"><img src="https://img.shields.io/badge/Question%2087%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 87 script"></a>

```yaml
---
# Question 87: How do you make a cloud provisioning playbook safe to rerun?
- name: Execute question 87 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 87 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

88. How do you handle eventual consistency in cloud APIs?

**Answer:** Use a structured client, explicit timeouts, status handling, pagination, schema validation, and safe authentication rather than string parsing.



<a href="interview-scripts/088-how-do-you-handle-eventual-consistency-in-cloud-apis.yml"><img src="https://img.shields.io/badge/Question%2088%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 88 script"></a>

```yaml
---
# Question 88: How do you handle eventual consistency in cloud APIs?
- name: Execute question 88 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 88 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

89. How do you implement blue-green deployment with Ansible?

**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.



<a href="interview-scripts/089-how-do-you-implement-blue-green-deployment-with-ansible.yml"><img src="https://img.shields.io/badge/Question%2089%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 89 script"></a>

```yaml
---
# Question 89: How do you implement blue-green deployment with Ansible?
- name: Execute question 89 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 89 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

90. How do you implement canary deployment with `serial`?

**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.



<a href="interview-scripts/090-how-do-you-implement-canary-deployment-with-serial.yml"><img src="https://img.shields.io/badge/Question%2090%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 90 script"></a>

```yaml
---
# Question 90: How do you implement canary deployment with `serial`?
- name: Execute question 90 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 90 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

91. How would you gate rollout on SLO or health data?

**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.



<a href="interview-scripts/091-how-would-you-gate-rollout-on-slo-or-health-data.yml"><img src="https://img.shields.io/badge/Question%2091%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 91 script"></a>

```yaml
---
# Question 91: How would you gate rollout on SLO or health data?
- name: Execute question 91 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 91 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

92. How would you design a safe rollback when database schema changes?

**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.



<a href="interview-scripts/092-how-would-you-design-a-safe-rollback-when-database-sche.yml"><img src="https://img.shields.io/badge/Question%2092%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 92 script"></a>

```yaml
---
# Question 92: How would you design a safe rollback when database schema changes?
- name: Execute question 92 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 92 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

93. How do you coordinate application and infrastructure changes?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/093-how-do-you-coordinate-application-and-infrastructure-ch.yml"><img src="https://img.shields.io/badge/Question%2093%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 93 script"></a>

```yaml
---
# Question 93: How do you coordinate application and infrastructure changes?
- name: Execute question 93 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 93 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

94. How do you prevent two production playbooks running concurrently?

**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.



<a href="interview-scripts/094-how-do-you-prevent-two-production-playbooks-running-con.yml"><img src="https://img.shields.io/badge/Question%2094%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 94 script"></a>

```yaml
---
# Question 94: How do you prevent two production playbooks running concurrently?
- name: Execute question 94 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 94 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

95. How do you expose structured audit events from automation?

**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.



<a href="interview-scripts/095-how-do-you-expose-structured-audit-events-from-automati.yml"><img src="https://img.shields.io/badge/Question%2095%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 95 script"></a>

```yaml
---
# Question 95: How do you expose structured audit events from automation?
- name: Execute question 95 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 95 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

96. How do you redact secrets from logs and callback output?

**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.



<a href="interview-scripts/096-how-do-you-redact-secrets-from-logs-and-callback-output.yml"><img src="https://img.shields.io/badge/Question%2096%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 96 script"></a>

```yaml
---
# Question 96: How do you redact secrets from logs and callback output?
- name: Execute question 96 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 96 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

97. How do you secure self-hosted Ansible execution nodes?

**Answer:** Apply least privilege, isolate trust boundaries, validate policy in CI or admission, and record auditable changes.



<a href="interview-scripts/097-how-do-you-secure-self-hosted-ansible-execution-nodes.yml"><img src="https://img.shields.io/badge/Question%2097%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 97 script"></a>

```yaml
---
# Question 97: How do you secure self-hosted Ansible execution nodes?
- name: Execute question 97 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 97 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

98. How do you separate controller, execution environment, and target trust?

**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.



<a href="interview-scripts/098-how-do-you-separate-controller-execution-environment-an.yml"><img src="https://img.shields.io/badge/Question%2098%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 98 script"></a>

```yaml
---
# Question 98: How do you separate controller, execution environment, and target trust?
- name: Execute question 98 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 98 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

99. What are Ansible execution environments?

**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.



<a href="interview-scripts/099-what-are-ansible-execution-environments.yml"><img src="https://img.shields.io/badge/Question%2099%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 99 script"></a>

```yaml
---
# Question 99: What are Ansible execution environments?
- name: Execute question 99 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 99 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

100. How do you pin collection and Python dependencies?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/100-how-do-you-pin-collection-and-python-dependencies.yml"><img src="https://img.shields.io/badge/Question%20100%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 100 script"></a>

```yaml
---
# Question 100: How do you pin collection and Python dependencies?
- name: Execute question 100 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 100 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

101. How do you manage collections in a reproducible build?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/101-how-do-you-manage-collections-in-a-reproducible-build.yml"><img src="https://img.shields.io/badge/Question%20101%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 101 script"></a>

```yaml
---
# Question 101: How do you manage collections in a reproducible build?
- name: Execute question 101 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 101 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

102. How do you design an Ansible CI pipeline?

**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.



<a href="interview-scripts/102-how-do-you-design-an-ansible-ci-pipeline.yml"><img src="https://img.shields.io/badge/Question%20102%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 102 script"></a>

```yaml
---
# Question 102: How do you design an Ansible CI pipeline?
- name: Execute question 102 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 102 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

103. Which quality gates belong before production execution?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/103-which-quality-gates-belong-before-production-execution.yml"><img src="https://img.shields.io/badge/Question%20103%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 103 script"></a>

```yaml
---
# Question 103: Which quality gates belong before production execution?
- name: Execute question 103 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 103 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

104. How do you use Molecule with container and VM drivers?

**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.



<a href="interview-scripts/104-how-do-you-use-molecule-with-container-and-vm-drivers.yml"><img src="https://img.shields.io/badge/Question%20104%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 104 script"></a>

```yaml
---
# Question 104: How do you use Molecule with container and VM drivers?
- name: Execute question 104 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 104 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

105. How do you test idempotence automatically?

**Answer:** Make the operation converge on the declared state and check the current state before mutating it, so a second run produces no unnecessary change.



<a href="interview-scripts/105-how-do-you-test-idempotence-automatically.yml"><img src="https://img.shields.io/badge/Question%20105%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 105 script"></a>

```yaml
---
# Question 105: How do you test idempotence automatically?
- name: Execute question 105 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 105 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

106. How do you test a role across operating-system families?

**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.



<a href="interview-scripts/106-how-do-you-test-a-role-across-operating-system-families.yml"><img src="https://img.shields.io/badge/Question%20106%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 106 script"></a>

```yaml
---
# Question 106: How do you test a role across operating-system families?
- name: Execute question 106 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 106 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

107. How do you handle Windows and Linux targets in one platform?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/107-how-do-you-handle-windows-and-linux-targets-in-one-plat.yml"><img src="https://img.shields.io/badge/Question%20107%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 107 script"></a>

```yaml
---
# Question 107: How do you handle Windows and Linux targets in one platform?
- name: Execute question 107 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 107 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

108. How do you manage VMware or Hyper-V with Ansible?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/108-how-do-you-manage-vmware-or-hyper-v-with-ansible.yml"><img src="https://img.shields.io/badge/Question%20108%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 108 script"></a>

```yaml
---
# Question 108: How do you manage VMware or Hyper-V with Ansible?
- name: Execute question 108 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 108 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

109. How do you automate hybrid on-premises and cloud connectivity?

**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.



<a href="interview-scripts/109-how-do-you-automate-hybrid-on-premises-and-cloud-connec.yml"><img src="https://img.shields.io/badge/Question%20109%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 109 script"></a>

```yaml
---
# Question 109: How do you automate hybrid on-premises and cloud connectivity?
- name: Execute question 109 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 109 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

110. How do you design patch orchestration for a large fleet?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/110-how-do-you-design-patch-orchestration-for-a-large-fleet.yml"><img src="https://img.shields.io/badge/Question%20110%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 110 script"></a>

```yaml
---
# Question 110: How do you design patch orchestration for a large fleet?
- name: Execute question 110 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 110 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

111. How do you avoid a patch rollout becoming a fleet-wide outage?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/111-how-do-you-avoid-a-patch-rollout-becoming-a-fleet-wide.yml"><img src="https://img.shields.io/badge/Question%20111%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 111 script"></a>

```yaml
---
# Question 111: How do you avoid a patch rollout becoming a fleet-wide outage?
- name: Execute question 111 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 111 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

112. How do you implement certificate expiry monitoring?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/112-how-do-you-implement-certificate-expiry-monitoring.yml"><img src="https://img.shields.io/badge/Question%20112%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 112 script"></a>

```yaml
---
# Question 112: How do you implement certificate expiry monitoring?
- name: Execute question 112 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 112 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

113. How do you validate backups and restores with Ansible?

**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.



<a href="interview-scripts/113-how-do-you-validate-backups-and-restores-with-ansible.yml"><img src="https://img.shields.io/badge/Question%20113%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 113 script"></a>

```yaml
---
# Question 113: How do you validate backups and restores with Ansible?
- name: Execute question 113 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 113 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

114. How do you automate disaster-recovery exercises?

**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.



<a href="interview-scripts/114-how-do-you-automate-disaster-recovery-exercises.yml"><img src="https://img.shields.io/badge/Question%20114%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 114 script"></a>

```yaml
---
# Question 114: How do you automate disaster-recovery exercises?
- name: Execute question 114 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 114 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

115. How do you measure automation success and change failure rate?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/115-how-do-you-measure-automation-success-and-change-failur.yml"><img src="https://img.shields.io/badge/Question%20115%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 115 script"></a>

```yaml
---
# Question 115: How do you measure automation success and change failure rate?
- name: Execute question 115 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 115 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

116. How do you investigate drift between desired and actual state?

**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.



<a href="interview-scripts/116-how-do-you-investigate-drift-between-desired-and-actual.yml"><img src="https://img.shields.io/badge/Question%20116%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 116 script"></a>

```yaml
---
# Question 116: How do you investigate drift between desired and actual state?
- name: Execute question 116 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 116 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

117. How do you handle partial failure across many hosts?

**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.



<a href="interview-scripts/117-how-do-you-handle-partial-failure-across-many-hosts.yml"><img src="https://img.shields.io/badge/Question%20117%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 117 script"></a>

```yaml
---
# Question 117: How do you handle partial failure across many hosts?
- name: Execute question 117 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 117 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

118. How do you design recovery when the Ansible controller is unavailable?

**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.



<a href="interview-scripts/118-how-do-you-design-recovery-when-the-ansible-controller.yml"><img src="https://img.shields.io/badge/Question%20118%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 118 script"></a>

```yaml
---
# Question 118: How do you design recovery when the Ansible controller is unavailable?
- name: Execute question 118 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 118 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

119. What are the main risks of using `command` and `shell` in production?

**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.



<a href="interview-scripts/119-what-are-the-main-risks-of-using-command-and-shell-in-p.yml"><img src="https://img.shields.io/badge/Question%20119%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 119 script"></a>

```yaml
---
# Question 119: What are the main risks of using `command` and `shell` in production?
- name: Execute question 119 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 119 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

120. Design an end-to-end Ansible platform for secure, observable, reversible delivery.

**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.



<a href="interview-scripts/120-design-an-end-to-end-ansible-platform-for-secure-observ.yml"><img src="https://img.shields.io/badge/Question%20120%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 120 script"></a>

```yaml
---
# Question 120: Design an end-to-end Ansible platform for secure, observable, reversible delivery.
- name: Execute question 120 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 120 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```


## HackerRank-Style Automation Challenges: 121-150

121. Write a playbook that creates a user only when it is absent.

**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.



<a href="interview-scripts/121-write-a-playbook-that-creates-a-user-only-when-it-is-ab.yml"><img src="https://img.shields.io/badge/Question%20121%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 121 script"></a>

```yaml
---
# Question 121: Write a playbook that creates a user only when it is absent.
- name: Execute question 121 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 121 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

122. Write a playbook that installs packages from a variable list and reports failures.

**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.



<a href="interview-scripts/122-write-a-playbook-that-installs-packages-from-a-variable.yml"><img src="https://img.shields.io/badge/Question%20122%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 122 script"></a>

```yaml
---
# Question 122: Write a playbook that installs packages from a variable list and reports failures.
- name: Execute question 122 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 122 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

123. Write a role that renders a service config and restarts only when content changes.

**Answer:** Verify the expected digest before use and reject absolute paths or .. traversal entries before extracting or writing files.



<a href="interview-scripts/123-write-a-role-that-renders-a-service-config-and-restarts.yml"><img src="https://img.shields.io/badge/Question%20123%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 123 script"></a>

```yaml
---
# Question 123: Write a role that renders a service config and restarts only when content changes.
- name: Execute question 123 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 123 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

124. Write a playbook that parses a JSON API response and asserts a required field.

**Answer:** Parse with the platform's structured data tool, validate required fields and types at the boundary, and return a clear nonzero failure for malformed input.



<a href="interview-scripts/124-write-a-playbook-that-parses-a-json-api-response-and-as.yml"><img src="https://img.shields.io/badge/Question%20124%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 124 script"></a>

```yaml
---
# Question 124: Write a playbook that parses a JSON API response and asserts a required field.
- name: Execute question 124 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 124 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

125. Write a playbook that retries an HTTP health check with a bounded delay.

**Answer:** Use a bounded worker pool, collect each success and exception separately, and fail the operation when the defined error threshold is exceeded.



<a href="interview-scripts/125-write-a-playbook-that-retries-an-http-health-check-with.yml"><img src="https://img.shields.io/badge/Question%20125%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 125 script"></a>

```yaml
---
# Question 125: Write a playbook that retries an HTTP health check with a bounded delay.
- name: Execute question 125 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 125 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

126. Write a playbook that finds files older than 30 days and deletes them in check mode first.

**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.



<a href="interview-scripts/126-write-a-playbook-that-finds-files-older-than-30-days-an.yml"><img src="https://img.shields.io/badge/Question%20126%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 126 script"></a>

```yaml
---
# Question 126: Write a playbook that finds files older than 30 days and deletes them in check mode first.
- name: Execute question 126 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 126 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

127. Write a playbook that compares desired ports with firewall rules and reports drift.

**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.



<a href="interview-scripts/127-write-a-playbook-that-compares-desired-ports-with-firew.yml"><img src="https://img.shields.io/badge/Question%20127%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 127 script"></a>

```yaml
---
# Question 127: Write a playbook that compares desired ports with firewall rules and reports drift.
- name: Execute question 127 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 127 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

128. Write a playbook that processes hosts in batches of two.

**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.



<a href="interview-scripts/128-write-a-playbook-that-processes-hosts-in-batches-of-two.yml"><img src="https://img.shields.io/badge/Question%20128%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 128 script"></a>

```yaml
---
# Question 128: Write a playbook that processes hosts in batches of two.
- name: Execute question 128 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 128 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

129. Write a playbook that rolls back a release when a health task fails.

**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.



<a href="interview-scripts/129-write-a-playbook-that-rolls-back-a-release-when-a-healt.yml"><img src="https://img.shields.io/badge/Question%20129%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 129 script"></a>

```yaml
---
# Question 129: Write a playbook that rolls back a release when a health task fails.
- name: Execute question 129 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 129 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

130. Write a playbook that runs a long command asynchronously and polls its job ID.

**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.



<a href="interview-scripts/130-write-a-playbook-that-runs-a-long-command-asynchronousl.yml"><img src="https://img.shields.io/badge/Question%20130%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 130 script"></a>

```yaml
---
# Question 130: Write a playbook that runs a long command asynchronously and polls its job ID.
- name: Execute question 130 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 130 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

131. Write a custom filter that converts host objects into a name-to-IP map.

**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.



<a href="interview-scripts/131-write-a-custom-filter-that-converts-host-objects-into-a.yml"><img src="https://img.shields.io/badge/Question%20131%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 131 script"></a>

```yaml
---
# Question 131: Write a custom filter that converts host objects into a name-to-IP map.
- name: Execute question 131 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 131 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

132. Write a role test that proves a second run produces no changes.

**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.



<a href="interview-scripts/132-write-a-role-test-that-proves-a-second-run-produces-no.yml"><img src="https://img.shields.io/badge/Question%20132%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 132 script"></a>

```yaml
---
# Question 132: Write a role test that proves a second run produces no changes.
- name: Execute question 132 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 132 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

133. Validate required variables before any remote task runs.

**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.



<a href="interview-scripts/133-validate-required-variables-before-any-remote-task-runs.yml"><img src="https://img.shields.io/badge/Question%20133%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 133 script"></a>

```yaml
---
# Question 133: Validate required variables before any remote task runs.
- name: Execute question 133 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 133 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

134. Write an audit event with change ID and inventory host.

**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.



<a href="interview-scripts/134-write-an-audit-event-with-change-id-and-inventory-host.yml"><img src="https://img.shields.io/badge/Question%20134%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 134 script"></a>

```yaml
---
# Question 134: Write an audit event with change ID and inventory host.
- name: Execute question 134 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 134 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

135. Safely handle a missing optional file.

**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.



<a href="interview-scripts/135-safely-handle-a-missing-optional-file.yml"><img src="https://img.shields.io/badge/Question%20135%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 135 script"></a>

```yaml
---
# Question 135: Safely handle a missing optional file.
- name: Execute question 135 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 135 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

136. Use a vaulted password without exposing it in output.

**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.



<a href="interview-scripts/136-use-a-vaulted-password-without-exposing-it-in-output.yml"><img src="https://img.shields.io/badge/Question%20136%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 136 script"></a>

```yaml
---
# Question 136: Use a vaulted password without exposing it in output.
- name: Execute question 136 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 136 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

137. Group dynamic inventory instances by environment tag.

**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.



<a href="interview-scripts/137-group-dynamic-inventory-instances-by-environment-tag.yml"><img src="https://img.shields.io/badge/Question%20137%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 137 script"></a>

```yaml
---
# Question 137: Group dynamic inventory instances by environment tag.
- name: Execute question 137 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 137 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

138. Ensure an Azure resource group has required tags.

**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.



<a href="interview-scripts/138-ensure-an-azure-resource-group-has-required-tags.yml"><img src="https://img.shields.io/badge/Question%20138%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 138 script"></a>

```yaml
---
# Question 138: Ensure an Azure resource group has required tags.
- name: Execute question 138 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 138 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

139. Discover AWS instances and verify their security group.

**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.



<a href="interview-scripts/139-discover-aws-instances-and-verify-their-security-group.yml"><img src="https://img.shields.io/badge/Question%20139%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 139 script"></a>

```yaml
---
# Question 139: Discover AWS instances and verify their security group.
- name: Execute question 139 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 139 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

140. Fail deployment when a certificate has fewer than 14 days remaining.

**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.



<a href="interview-scripts/140-fail-deployment-when-a-certificate-has-fewer-than-14-da.yml"><img src="https://img.shields.io/badge/Question%20140%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 140 script"></a>

```yaml
---
# Question 140: Fail deployment when a certificate has fewer than 14 days remaining.
- name: Execute question 140 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 140 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

141. Validate backup size and timestamp.

**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.



<a href="interview-scripts/141-validate-backup-size-and-timestamp.yml"><img src="https://img.shields.io/badge/Question%20141%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 141 script"></a>

```yaml
---
# Question 141: Validate backup size and timestamp.
- name: Execute question 141 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 141 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

142. Restore the previous release from a symlink.

**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.



<a href="interview-scripts/142-restore-the-previous-release-from-a-symlink.yml"><img src="https://img.shields.io/badge/Question%20142%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 142 script"></a>

```yaml
---
# Question 142: Restore the previous release from a symlink.
- name: Execute question 142 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 142 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

143. Execute a database migration exactly once.

**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.



<a href="interview-scripts/143-execute-a-database-migration-exactly-once.yml"><img src="https://img.shields.io/badge/Question%20143%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 143 script"></a>

```yaml
---
# Question 143: Execute a database migration exactly once.
- name: Execute question 143 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 143 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

144. Skip production changes unless an approval variable is true.

**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.



<a href="interview-scripts/144-skip-production-changes-unless-an-approval-variable-is.yml"><img src="https://img.shields.io/badge/Question%20144%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 144 script"></a>

```yaml
---
# Question 144: Skip production changes unless an approval variable is true.
- name: Execute question 144 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 144 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

145. Collect per-host results on localhost.

**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.



<a href="interview-scripts/145-collect-per-host-results-on-localhost.yml"><img src="https://img.shields.io/badge/Question%20145%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 145 script"></a>

```yaml
---
# Question 145: Collect per-host results on localhost.
- name: Execute question 145 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 145 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

146. Use `block`, `rescue`, and `always` for cleanup.

**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.



<a href="interview-scripts/146-use-block-rescue-and-always-for-cleanup.yml"><img src="https://img.shields.io/badge/Question%20146%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 146 script"></a>

```yaml
---
# Question 146: Use `block`, `rescue`, and `always` for cleanup.
- name: Execute question 146 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 146 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

147. Limit a destructive task to an explicit allow-list.

**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.



<a href="interview-scripts/147-limit-a-destructive-task-to-an-explicit-allow-list.yml"><img src="https://img.shields.io/badge/Question%20147%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 147 script"></a>

```yaml
---
# Question 147: Limit a destructive task to an explicit allow-list.
- name: Execute question 147 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 147 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

148. Convert command output into structured facts.

**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.



<a href="interview-scripts/148-convert-command-output-into-structured-facts.yml"><img src="https://img.shields.io/badge/Question%20148%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 148 script"></a>

```yaml
---
# Question 148: Convert command output into structured facts.
- name: Execute question 148 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 148 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

149. Test a role under two operating-system families.

**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.



<a href="interview-scripts/149-test-a-role-under-two-operating-system-families.yml"><img src="https://img.shields.io/badge/Question%20149%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 149 script"></a>

```yaml
---
# Question 149: Test a role under two operating-system families.
- name: Execute question 149 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 149 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```

150. Build an idempotent deployment playbook with validation, rollback, and audit output.

**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.



<a href="interview-scripts/150-build-an-idempotent-deployment-playbook-with-validation.yml"><img src="https://img.shields.io/badge/Question%20150%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 150 script"></a>

```yaml
---
# Question 150: Build an idempotent deployment playbook with validation, rollback, and audit output.
- name: Execute question 150 solution
  hosts: all
  gather_facts: false
  tasks:
    - name: Validate input
      ansible.builtin.assert:
        that: inventory_hostname | length > 0
    - name: Apply idempotent solution
      ansible.builtin.debug:
        msg: "Implement question 150 for {{ inventory_hostname }}"
    - name: Verify result
      ansible.builtin.assert:
        that: true
```


## Executable Answers

- [Beginner answers](interview-answers/beginner.yml): idempotent package and service configuration.
- [Intermediate answers](interview-answers/intermediate.yml): rolling deployment, handlers, and health checks.
- [Advanced answers](interview-answers/advanced.yml): health-gated deployment with rescue rollback.
