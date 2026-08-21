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
2. How does Ansible differ from agent-based configuration tools?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
3. What is an Ansible inventory?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
4. What is the difference between a host and a group?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
5. What is a playbook?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
6. What is a play?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
7. What is a task?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
8. What is a module?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
9. What is a fully qualified collection name?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
10. What does idempotence mean in Ansible?
**Answer:** Make the operation converge on the declared state and check the current state before mutating it, so a second run produces no unnecessary change.
11. Why should `ansible.builtin.command` be used carefully?
**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.
12. When would you use the `shell` module?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
13. What does `ansible.builtin.ping` actually verify?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
14. How do you run a playbook in check mode?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
15. What does `--diff` show?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
16. How do you pass an extra variable at runtime?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
17. What is the difference between `vars` and `vars_files`?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.
18. How do you use a variable in a task?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
19. What is a loop and how is it written?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
20. How do you register task output?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
21. What is a handler?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
22. When does a handler run?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
23. How do you notify a handler?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
24. How do `when` conditions work?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
25. How do you install a package portably?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
26. How do you manage a service?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
27. How do you create a user with Ansible?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
28. How do you copy a static file?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.
29. When should you use `template` instead of `copy`?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
30. What is privilege escalation with `become`?
**Answer:** Apply least privilege, isolate trust boundaries, validate policy in CI or admission, and record auditable changes.
31. How do you limit execution to selected hosts?
**Answer:** Declare requests and limits, measure real usage, set explicit capacity bounds, and test behavior under saturation and recovery.
32. What does `gather_facts` do?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
33. How do you print a variable for troubleshooting?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
34. How do you use tags?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
35. What is YAML indentation significance?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
36. How do you check playbook syntax?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
37. What is the difference between a changed and failed task?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
38. How do you make a command task report no change?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
39. What is an Ansible role?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
40. What information belongs in an inventory file?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.

## Intermediate: 41-80

41. Explain Ansible variable precedence with an example.
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
42. How do role defaults differ from role vars?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
43. What belongs in `tasks`, `handlers`, `templates`, and `defaults`?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
44. How do you design a reusable role?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
45. How do role dependencies work?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
46. How do you use `include_tasks` and `import_tasks`?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
47. When should you use a dynamic include?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
48. How do you loop over a block of tasks?
**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.
49. How do you combine registered results from a loop?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
50. How do you use `changed_when` correctly?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
51. How do you use `failed_when` safely?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
52. Explain `block`, `rescue`, and `always`.
**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.
53. How do you implement rollback after a failed deployment?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
54. What does `serial` do during a rolling deployment?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
55. How do `max_fail_percentage` and `any_errors_fatal` differ?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
56. What is the difference between `linear` and `free` strategy?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
57. How do you delegate a task to localhost?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
58. How do you share facts between hosts?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
59. How do you run long jobs asynchronously?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
60. How do you poll an asynchronous job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
61. How does `run_once` affect a task?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
62. How do you validate a rendered configuration before replacing it?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
63. How do you use `assert` to validate inputs?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
64. How do you wait for a service or port?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
65. How do you perform an HTTP health check?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
66. How do you find files older than a retention period?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.
67. How do you safely remove old releases?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
68. How do you manage line-based configuration?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
69. How do you preserve secrets with Ansible Vault?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
70. How should Vault passwords be supplied in CI?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
71. What is a lookup plugin?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
72. What is a filter plugin?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
73. How do you transform data with Jinja filters?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
74. How do you use `set_fact` without creating confusing state?
**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.
75. How do you pass environment variables to a task?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
76. How do you use check mode in custom commands?
**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.
77. How do you test a role with Molecule?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
78. How do Ansible lint and syntax check differ?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
79. How do you troubleshoot an unreachable host?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
80. How do you design inventories for dev, test, and production?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.

## Advanced: 81-120

81. How would you design Ansible for a multi-account Azure estate?
**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.
82. How would you design Ansible for multiple AWS accounts and regions?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
83. How do dynamic inventory plugins discover cloud hosts?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
84. How do you authenticate to Azure without long-lived secrets?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
85. How do you authenticate to AWS through an assumed role?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
86. How do you enforce cloud resource tags with Ansible?
**Answer:** Declare requests and limits, measure real usage, set explicit capacity bounds, and test behavior under saturation and recovery.
87. How do you make a cloud provisioning playbook safe to rerun?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
88. How do you handle eventual consistency in cloud APIs?
**Answer:** Use a structured client, explicit timeouts, status handling, pagination, schema validation, and safe authentication rather than string parsing.
89. How do you implement blue-green deployment with Ansible?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
90. How do you implement canary deployment with `serial`?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
91. How would you gate rollout on SLO or health data?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
92. How would you design a safe rollback when database schema changes?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
93. How do you coordinate application and infrastructure changes?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
94. How do you prevent two production playbooks running concurrently?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
95. How do you expose structured audit events from automation?
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
96. How do you redact secrets from logs and callback output?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
97. How do you secure self-hosted Ansible execution nodes?
**Answer:** Apply least privilege, isolate trust boundaries, validate policy in CI or admission, and record auditable changes.
98. How do you separate controller, execution environment, and target trust?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
99. What are Ansible execution environments?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
100. How do you pin collection and Python dependencies?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
101. How do you manage collections in a reproducible build?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
102. How do you design an Ansible CI pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
103. Which quality gates belong before production execution?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
104. How do you use Molecule with container and VM drivers?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
105. How do you test idempotence automatically?
**Answer:** Make the operation converge on the declared state and check the current state before mutating it, so a second run produces no unnecessary change.
106. How do you test a role across operating-system families?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
107. How do you handle Windows and Linux targets in one platform?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
108. How do you manage VMware or Hyper-V with Ansible?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
109. How do you automate hybrid on-premises and cloud connectivity?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
110. How do you design patch orchestration for a large fleet?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
111. How do you avoid a patch rollout becoming a fleet-wide outage?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
112. How do you implement certificate expiry monitoring?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
113. How do you validate backups and restores with Ansible?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
114. How do you automate disaster-recovery exercises?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
115. How do you measure automation success and change failure rate?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
116. How do you investigate drift between desired and actual state?
**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.
117. How do you handle partial failure across many hosts?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
118. How do you design recovery when the Ansible controller is unavailable?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
119. What are the main risks of using `command` and `shell` in production?
**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.
120. Design an end-to-end Ansible platform for secure, observable, reversible delivery.
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.

## HackerRank-Style Automation Challenges: 121-150

121. Write a playbook that creates a user only when it is absent.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
122. Write a playbook that installs packages from a variable list and reports failures.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
123. Write a role that renders a service config and restarts only when content changes.
**Answer:** Verify the expected digest before use and reject absolute paths or .. traversal entries before extracting or writing files.
124. Write a playbook that parses a JSON API response and asserts a required field.
**Answer:** Parse with the platform's structured data tool, validate required fields and types at the boundary, and return a clear nonzero failure for malformed input.
125. Write a playbook that retries an HTTP health check with a bounded delay.
**Answer:** Use a bounded worker pool, collect each success and exception separately, and fail the operation when the defined error threshold is exceeded.
126. Write a playbook that finds files older than 30 days and deletes them in check mode first.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
127. Write a playbook that compares desired ports with firewall rules and reports drift.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
128. Write a playbook that processes hosts in batches of two.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
129. Write a playbook that rolls back a release when a health task fails.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
130. Write a playbook that runs a long command asynchronously and polls its job ID.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
131. Write a custom filter that converts host objects into a name-to-IP map.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
132. Write a role test that proves a second run produces no changes.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
133. Validate required variables before any remote task runs.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
134. Write an audit event with change ID and inventory host.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
135. Safely handle a missing optional file.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
136. Use a vaulted password without exposing it in output.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
137. Group dynamic inventory instances by environment tag.
**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.
138. Ensure an Azure resource group has required tags.
**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.
139. Discover AWS instances and verify their security group.
**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.
140. Fail deployment when a certificate has fewer than 14 days remaining.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
141. Validate backup size and timestamp.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
142. Restore the previous release from a symlink.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
143. Execute a database migration exactly once.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
144. Skip production changes unless an approval variable is true.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
145. Collect per-host results on localhost.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
146. Use `block`, `rescue`, and `always` for cleanup.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
147. Limit a destructive task to an explicit allow-list.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
148. Convert command output into structured facts.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
149. Test a role under two operating-system families.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
150. Build an idempotent deployment playbook with validation, rollback, and audit output.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.

## Executable Answers

- [Beginner answers](interview-answers/beginner.yml): idempotent package and service configuration.
- [Intermediate answers](interview-answers/intermediate.yml): rolling deployment, handlers, and health checks.
- [Advanced answers](interview-answers/advanced.yml): health-gated deployment with rescue rollback.
