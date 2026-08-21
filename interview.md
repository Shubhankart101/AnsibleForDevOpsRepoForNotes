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
Script: [Question 1 script](interview-scripts/001-what-problem-does-ansible-solve.yml)
2. How does Ansible differ from agent-based configuration tools?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 2 script](interview-scripts/002-how-does-ansible-differ-from-agent-based-configuration.yml)
3. What is an Ansible inventory?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 3 script](interview-scripts/003-what-is-an-ansible-inventory.yml)
4. What is the difference between a host and a group?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 4 script](interview-scripts/004-what-is-the-difference-between-a-host-and-a-group.yml)
5. What is a playbook?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 5 script](interview-scripts/005-what-is-a-playbook.yml)
6. What is a play?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 6 script](interview-scripts/006-what-is-a-play.yml)
7. What is a task?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 7 script](interview-scripts/007-what-is-a-task.yml)
8. What is a module?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 8 script](interview-scripts/008-what-is-a-module.yml)
9. What is a fully qualified collection name?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 9 script](interview-scripts/009-what-is-a-fully-qualified-collection-name.yml)
10. What does idempotence mean in Ansible?
**Answer:** Make the operation converge on the declared state and check the current state before mutating it, so a second run produces no unnecessary change.
Script: [Question 10 script](interview-scripts/010-what-does-idempotence-mean-in-ansible.yml)
11. Why should `ansible.builtin.command` be used carefully?
**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.
Script: [Question 11 script](interview-scripts/011-why-should-ansible-builtin-command-be-used-carefully.yml)
12. When would you use the `shell` module?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 12 script](interview-scripts/012-when-would-you-use-the-shell-module.yml)
13. What does `ansible.builtin.ping` actually verify?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 13 script](interview-scripts/013-what-does-ansible-builtin-ping-actually-verify.yml)
14. How do you run a playbook in check mode?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 14 script](interview-scripts/014-how-do-you-run-a-playbook-in-check-mode.yml)
15. What does `--diff` show?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 15 script](interview-scripts/015-what-does-diff-show.yml)
16. How do you pass an extra variable at runtime?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 16 script](interview-scripts/016-how-do-you-pass-an-extra-variable-at-runtime.yml)
17. What is the difference between `vars` and `vars_files`?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.
Script: [Question 17 script](interview-scripts/017-what-is-the-difference-between-vars-and-vars-files.yml)
18. How do you use a variable in a task?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 18 script](interview-scripts/018-how-do-you-use-a-variable-in-a-task.yml)
19. What is a loop and how is it written?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 19 script](interview-scripts/019-what-is-a-loop-and-how-is-it-written.yml)
20. How do you register task output?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 20 script](interview-scripts/020-how-do-you-register-task-output.yml)
21. What is a handler?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 21 script](interview-scripts/021-what-is-a-handler.yml)
22. When does a handler run?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 22 script](interview-scripts/022-when-does-a-handler-run.yml)
23. How do you notify a handler?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 23 script](interview-scripts/023-how-do-you-notify-a-handler.yml)
24. How do `when` conditions work?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 24 script](interview-scripts/024-how-do-when-conditions-work.yml)
25. How do you install a package portably?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
Script: [Question 25 script](interview-scripts/025-how-do-you-install-a-package-portably.yml)
26. How do you manage a service?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
Script: [Question 26 script](interview-scripts/026-how-do-you-manage-a-service.yml)
27. How do you create a user with Ansible?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 27 script](interview-scripts/027-how-do-you-create-a-user-with-ansible.yml)
28. How do you copy a static file?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.
Script: [Question 28 script](interview-scripts/028-how-do-you-copy-a-static-file.yml)
29. When should you use `template` instead of `copy`?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 29 script](interview-scripts/029-when-should-you-use-template-instead-of-copy.yml)
30. What is privilege escalation with `become`?
**Answer:** Apply least privilege, isolate trust boundaries, validate policy in CI or admission, and record auditable changes.
Script: [Question 30 script](interview-scripts/030-what-is-privilege-escalation-with-become.yml)
31. How do you limit execution to selected hosts?
**Answer:** Declare requests and limits, measure real usage, set explicit capacity bounds, and test behavior under saturation and recovery.
Script: [Question 31 script](interview-scripts/031-how-do-you-limit-execution-to-selected-hosts.yml)
32. What does `gather_facts` do?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 32 script](interview-scripts/032-what-does-gather-facts-do.yml)
33. How do you print a variable for troubleshooting?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 33 script](interview-scripts/033-how-do-you-print-a-variable-for-troubleshooting.yml)
34. How do you use tags?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 34 script](interview-scripts/034-how-do-you-use-tags.yml)
35. What is YAML indentation significance?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 35 script](interview-scripts/035-what-is-yaml-indentation-significance.yml)
36. How do you check playbook syntax?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 36 script](interview-scripts/036-how-do-you-check-playbook-syntax.yml)
37. What is the difference between a changed and failed task?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 37 script](interview-scripts/037-what-is-the-difference-between-a-changed-and-failed-tas.yml)
38. How do you make a command task report no change?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
Script: [Question 38 script](interview-scripts/038-how-do-you-make-a-command-task-report-no-change.yml)
39. What is an Ansible role?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 39 script](interview-scripts/039-what-is-an-ansible-role.yml)
40. What information belongs in an inventory file?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.
Script: [Question 40 script](interview-scripts/040-what-information-belongs-in-an-inventory-file.yml)

## Intermediate: 41-80

41. Explain Ansible variable precedence with an example.
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 41 script](interview-scripts/041-explain-ansible-variable-precedence-with-an-example.yml)
42. How do role defaults differ from role vars?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 42 script](interview-scripts/042-how-do-role-defaults-differ-from-role-vars.yml)
43. What belongs in `tasks`, `handlers`, `templates`, and `defaults`?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 43 script](interview-scripts/043-what-belongs-in-tasks-handlers-templates-and-defaults.yml)
44. How do you design a reusable role?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 44 script](interview-scripts/044-how-do-you-design-a-reusable-role.yml)
45. How do role dependencies work?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 45 script](interview-scripts/045-how-do-role-dependencies-work.yml)
46. How do you use `include_tasks` and `import_tasks`?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
Script: [Question 46 script](interview-scripts/046-how-do-you-use-include-tasks-and-import-tasks.yml)
47. When should you use a dynamic include?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 47 script](interview-scripts/047-when-should-you-use-a-dynamic-include.yml)
48. How do you loop over a block of tasks?
**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.
Script: [Question 48 script](interview-scripts/048-how-do-you-loop-over-a-block-of-tasks.yml)
49. How do you combine registered results from a loop?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 49 script](interview-scripts/049-how-do-you-combine-registered-results-from-a-loop.yml)
50. How do you use `changed_when` correctly?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 50 script](interview-scripts/050-how-do-you-use-changed-when-correctly.yml)
51. How do you use `failed_when` safely?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 51 script](interview-scripts/051-how-do-you-use-failed-when-safely.yml)
52. Explain `block`, `rescue`, and `always`.
**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.
Script: [Question 52 script](interview-scripts/052-explain-block-rescue-and-always.yml)
53. How do you implement rollback after a failed deployment?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
Script: [Question 53 script](interview-scripts/053-how-do-you-implement-rollback-after-a-failed-deployment.yml)
54. What does `serial` do during a rolling deployment?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 54 script](interview-scripts/054-what-does-serial-do-during-a-rolling-deployment.yml)
55. How do `max_fail_percentage` and `any_errors_fatal` differ?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 55 script](interview-scripts/055-how-do-max-fail-percentage-and-any-errors-fatal-differ.yml)
56. What is the difference between `linear` and `free` strategy?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 56 script](interview-scripts/056-what-is-the-difference-between-linear-and-free-strategy.yml)
57. How do you delegate a task to localhost?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 57 script](interview-scripts/057-how-do-you-delegate-a-task-to-localhost.yml)
58. How do you share facts between hosts?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 58 script](interview-scripts/058-how-do-you-share-facts-between-hosts.yml)
59. How do you run long jobs asynchronously?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 59 script](interview-scripts/059-how-do-you-run-long-jobs-asynchronously.yml)
60. How do you poll an asynchronous job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 60 script](interview-scripts/060-how-do-you-poll-an-asynchronous-job.yml)
61. How does `run_once` affect a task?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 61 script](interview-scripts/061-how-does-run-once-affect-a-task.yml)
62. How do you validate a rendered configuration before replacing it?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 62 script](interview-scripts/062-how-do-you-validate-a-rendered-configuration-before-rep.yml)
63. How do you use `assert` to validate inputs?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 63 script](interview-scripts/063-how-do-you-use-assert-to-validate-inputs.yml)
64. How do you wait for a service or port?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
Script: [Question 64 script](interview-scripts/064-how-do-you-wait-for-a-service-or-port.yml)
65. How do you perform an HTTP health check?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
Script: [Question 65 script](interview-scripts/065-how-do-you-perform-an-http-health-check.yml)
66. How do you find files older than a retention period?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.
Script: [Question 66 script](interview-scripts/066-how-do-you-find-files-older-than-a-retention-period.yml)
67. How do you safely remove old releases?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 67 script](interview-scripts/067-how-do-you-safely-remove-old-releases.yml)
68. How do you manage line-based configuration?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 68 script](interview-scripts/068-how-do-you-manage-line-based-configuration.yml)
69. How do you preserve secrets with Ansible Vault?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 69 script](interview-scripts/069-how-do-you-preserve-secrets-with-ansible-vault.yml)
70. How should Vault passwords be supplied in CI?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 70 script](interview-scripts/070-how-should-vault-passwords-be-supplied-in-ci.yml)
71. What is a lookup plugin?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 71 script](interview-scripts/071-what-is-a-lookup-plugin.yml)
72. What is a filter plugin?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 72 script](interview-scripts/072-what-is-a-filter-plugin.yml)
73. How do you transform data with Jinja filters?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 73 script](interview-scripts/073-how-do-you-transform-data-with-jinja-filters.yml)
74. How do you use `set_fact` without creating confusing state?
**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.
Script: [Question 74 script](interview-scripts/074-how-do-you-use-set-fact-without-creating-confusing-stat.yml)
75. How do you pass environment variables to a task?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 75 script](interview-scripts/075-how-do-you-pass-environment-variables-to-a-task.yml)
76. How do you use check mode in custom commands?
**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.
Script: [Question 76 script](interview-scripts/076-how-do-you-use-check-mode-in-custom-commands.yml)
77. How do you test a role with Molecule?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 77 script](interview-scripts/077-how-do-you-test-a-role-with-molecule.yml)
78. How do Ansible lint and syntax check differ?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 78 script](interview-scripts/078-how-do-ansible-lint-and-syntax-check-differ.yml)
79. How do you troubleshoot an unreachable host?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 79 script](interview-scripts/079-how-do-you-troubleshoot-an-unreachable-host.yml)
80. How do you design inventories for dev, test, and production?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 80 script](interview-scripts/080-how-do-you-design-inventories-for-dev-test-and-producti.yml)

## Advanced: 81-120

81. How would you design Ansible for a multi-account Azure estate?
**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.
Script: [Question 81 script](interview-scripts/081-how-would-you-design-ansible-for-a-multi-account-azure.yml)
82. How would you design Ansible for multiple AWS accounts and regions?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
Script: [Question 82 script](interview-scripts/082-how-would-you-design-ansible-for-multiple-aws-accounts.yml)
83. How do dynamic inventory plugins discover cloud hosts?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
Script: [Question 83 script](interview-scripts/083-how-do-dynamic-inventory-plugins-discover-cloud-hosts.yml)
84. How do you authenticate to Azure without long-lived secrets?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 84 script](interview-scripts/084-how-do-you-authenticate-to-azure-without-long-lived-sec.yml)
85. How do you authenticate to AWS through an assumed role?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 85 script](interview-scripts/085-how-do-you-authenticate-to-aws-through-an-assumed-role.yml)
86. How do you enforce cloud resource tags with Ansible?
**Answer:** Declare requests and limits, measure real usage, set explicit capacity bounds, and test behavior under saturation and recovery.
Script: [Question 86 script](interview-scripts/086-how-do-you-enforce-cloud-resource-tags-with-ansible.yml)
87. How do you make a cloud provisioning playbook safe to rerun?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
Script: [Question 87 script](interview-scripts/087-how-do-you-make-a-cloud-provisioning-playbook-safe-to-r.yml)
88. How do you handle eventual consistency in cloud APIs?
**Answer:** Use a structured client, explicit timeouts, status handling, pagination, schema validation, and safe authentication rather than string parsing.
Script: [Question 88 script](interview-scripts/088-how-do-you-handle-eventual-consistency-in-cloud-apis.yml)
89. How do you implement blue-green deployment with Ansible?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 89 script](interview-scripts/089-how-do-you-implement-blue-green-deployment-with-ansible.yml)
90. How do you implement canary deployment with `serial`?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 90 script](interview-scripts/090-how-do-you-implement-canary-deployment-with-serial.yml)
91. How would you gate rollout on SLO or health data?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
Script: [Question 91 script](interview-scripts/091-how-would-you-gate-rollout-on-slo-or-health-data.yml)
92. How would you design a safe rollback when database schema changes?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
Script: [Question 92 script](interview-scripts/092-how-would-you-design-a-safe-rollback-when-database-sche.yml)
93. How do you coordinate application and infrastructure changes?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 93 script](interview-scripts/093-how-do-you-coordinate-application-and-infrastructure-ch.yml)
94. How do you prevent two production playbooks running concurrently?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 94 script](interview-scripts/094-how-do-you-prevent-two-production-playbooks-running-con.yml)
95. How do you expose structured audit events from automation?
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
Script: [Question 95 script](interview-scripts/095-how-do-you-expose-structured-audit-events-from-automati.yml)
96. How do you redact secrets from logs and callback output?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 96 script](interview-scripts/096-how-do-you-redact-secrets-from-logs-and-callback-output.yml)
97. How do you secure self-hosted Ansible execution nodes?
**Answer:** Apply least privilege, isolate trust boundaries, validate policy in CI or admission, and record auditable changes.
Script: [Question 97 script](interview-scripts/097-how-do-you-secure-self-hosted-ansible-execution-nodes.yml)
98. How do you separate controller, execution environment, and target trust?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 98 script](interview-scripts/098-how-do-you-separate-controller-execution-environment-an.yml)
99. What are Ansible execution environments?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 99 script](interview-scripts/099-what-are-ansible-execution-environments.yml)
100. How do you pin collection and Python dependencies?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 100 script](interview-scripts/100-how-do-you-pin-collection-and-python-dependencies.yml)
101. How do you manage collections in a reproducible build?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 101 script](interview-scripts/101-how-do-you-manage-collections-in-a-reproducible-build.yml)
102. How do you design an Ansible CI pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 102 script](interview-scripts/102-how-do-you-design-an-ansible-ci-pipeline.yml)
103. Which quality gates belong before production execution?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 103 script](interview-scripts/103-which-quality-gates-belong-before-production-execution.yml)
104. How do you use Molecule with container and VM drivers?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 104 script](interview-scripts/104-how-do-you-use-molecule-with-container-and-vm-drivers.yml)
105. How do you test idempotence automatically?
**Answer:** Make the operation converge on the declared state and check the current state before mutating it, so a second run produces no unnecessary change.
Script: [Question 105 script](interview-scripts/105-how-do-you-test-idempotence-automatically.yml)
106. How do you test a role across operating-system families?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 106 script](interview-scripts/106-how-do-you-test-a-role-across-operating-system-families.yml)
107. How do you handle Windows and Linux targets in one platform?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 107 script](interview-scripts/107-how-do-you-handle-windows-and-linux-targets-in-one-plat.yml)
108. How do you manage VMware or Hyper-V with Ansible?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 108 script](interview-scripts/108-how-do-you-manage-vmware-or-hyper-v-with-ansible.yml)
109. How do you automate hybrid on-premises and cloud connectivity?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
Script: [Question 109 script](interview-scripts/109-how-do-you-automate-hybrid-on-premises-and-cloud-connec.yml)
110. How do you design patch orchestration for a large fleet?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 110 script](interview-scripts/110-how-do-you-design-patch-orchestration-for-a-large-fleet.yml)
111. How do you avoid a patch rollout becoming a fleet-wide outage?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 111 script](interview-scripts/111-how-do-you-avoid-a-patch-rollout-becoming-a-fleet-wide.yml)
112. How do you implement certificate expiry monitoring?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 112 script](interview-scripts/112-how-do-you-implement-certificate-expiry-monitoring.yml)
113. How do you validate backups and restores with Ansible?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
Script: [Question 113 script](interview-scripts/113-how-do-you-validate-backups-and-restores-with-ansible.yml)
114. How do you automate disaster-recovery exercises?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
Script: [Question 114 script](interview-scripts/114-how-do-you-automate-disaster-recovery-exercises.yml)
115. How do you measure automation success and change failure rate?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 115 script](interview-scripts/115-how-do-you-measure-automation-success-and-change-failur.yml)
116. How do you investigate drift between desired and actual state?
**Answer:** Store shared state remotely with encryption, access control, locking, versioning, and a tested recovery process.
Script: [Question 116 script](interview-scripts/116-how-do-you-investigate-drift-between-desired-and-actual.yml)
117. How do you handle partial failure across many hosts?
**Answer:** A strong answer should define the concept, show a small Ansible implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 117 script](interview-scripts/117-how-do-you-handle-partial-failure-across-many-hosts.yml)
118. How do you design recovery when the Ansible controller is unavailable?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
Script: [Question 118 script](interview-scripts/118-how-do-you-design-recovery-when-the-ansible-controller.yml)
119. What are the main risks of using `command` and `shell` in production?
**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.
Script: [Question 119 script](interview-scripts/119-what-are-the-main-risks-of-using-command-and-shell-in-p.yml)
120. Design an end-to-end Ansible platform for secure, observable, reversible delivery.
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
Script: [Question 120 script](interview-scripts/120-design-an-end-to-end-ansible-platform-for-secure-observ.yml)

## HackerRank-Style Automation Challenges: 121-150

121. Write a playbook that creates a user only when it is absent.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
Script: [Question 121 script](interview-scripts/121-write-a-playbook-that-creates-a-user-only-when-it-is-ab.yml)
122. Write a playbook that installs packages from a variable list and reports failures.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
Script: [Question 122 script](interview-scripts/122-write-a-playbook-that-installs-packages-from-a-variable.yml)
123. Write a role that renders a service config and restarts only when content changes.
**Answer:** Verify the expected digest before use and reject absolute paths or .. traversal entries before extracting or writing files.
Script: [Question 123 script](interview-scripts/123-write-a-role-that-renders-a-service-config-and-restarts.yml)
124. Write a playbook that parses a JSON API response and asserts a required field.
**Answer:** Parse with the platform's structured data tool, validate required fields and types at the boundary, and return a clear nonzero failure for malformed input.
Script: [Question 124 script](interview-scripts/124-write-a-playbook-that-parses-a-json-api-response-and-as.yml)
125. Write a playbook that retries an HTTP health check with a bounded delay.
**Answer:** Use a bounded worker pool, collect each success and exception separately, and fail the operation when the defined error threshold is exceeded.
Script: [Question 125 script](interview-scripts/125-write-a-playbook-that-retries-an-http-health-check-with.yml)
126. Write a playbook that finds files older than 30 days and deletes them in check mode first.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
Script: [Question 126 script](interview-scripts/126-write-a-playbook-that-finds-files-older-than-30-days-an.yml)
127. Write a playbook that compares desired ports with firewall rules and reports drift.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
Script: [Question 127 script](interview-scripts/127-write-a-playbook-that-compares-desired-ports-with-firew.yml)
128. Write a playbook that processes hosts in batches of two.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
Script: [Question 128 script](interview-scripts/128-write-a-playbook-that-processes-hosts-in-batches-of-two.yml)
129. Write a playbook that rolls back a release when a health task fails.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 129 script](interview-scripts/129-write-a-playbook-that-rolls-back-a-release-when-a-healt.yml)
130. Write a playbook that runs a long command asynchronously and polls its job ID.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 130 script](interview-scripts/130-write-a-playbook-that-runs-a-long-command-asynchronousl.yml)
131. Write a custom filter that converts host objects into a name-to-IP map.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
Script: [Question 131 script](interview-scripts/131-write-a-custom-filter-that-converts-host-objects-into-a.yml)
132. Write a role test that proves a second run produces no changes.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
Script: [Question 132 script](interview-scripts/132-write-a-role-test-that-proves-a-second-run-produces-no.yml)
133. Validate required variables before any remote task runs.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
Script: [Question 133 script](interview-scripts/133-validate-required-variables-before-any-remote-task-runs.yml)
134. Write an audit event with change ID and inventory host.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
Script: [Question 134 script](interview-scripts/134-write-an-audit-event-with-change-id-and-inventory-host.yml)
135. Safely handle a missing optional file.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
Script: [Question 135 script](interview-scripts/135-safely-handle-a-missing-optional-file.yml)
136. Use a vaulted password without exposing it in output.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
Script: [Question 136 script](interview-scripts/136-use-a-vaulted-password-without-exposing-it-in-output.yml)
137. Group dynamic inventory instances by environment tag.
**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.
Script: [Question 137 script](interview-scripts/137-group-dynamic-inventory-instances-by-environment-tag.yml)
138. Ensure an Azure resource group has required tags.
**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.
Script: [Question 138 script](interview-scripts/138-ensure-an-azure-resource-group-has-required-tags.yml)
139. Discover AWS instances and verify their security group.
**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.
Script: [Question 139 script](interview-scripts/139-discover-aws-instances-and-verify-their-security-group.yml)
140. Fail deployment when a certificate has fewer than 14 days remaining.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 140 script](interview-scripts/140-fail-deployment-when-a-certificate-has-fewer-than-14-da.yml)
141. Validate backup size and timestamp.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
Script: [Question 141 script](interview-scripts/141-validate-backup-size-and-timestamp.yml)
142. Restore the previous release from a symlink.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 142 script](interview-scripts/142-restore-the-previous-release-from-a-symlink.yml)
143. Execute a database migration exactly once.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
Script: [Question 143 script](interview-scripts/143-execute-a-database-migration-exactly-once.yml)
144. Skip production changes unless an approval variable is true.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
Script: [Question 144 script](interview-scripts/144-skip-production-changes-unless-an-approval-variable-is.yml)
145. Collect per-host results on localhost.
**Answer:** Use an idempotent module or role, validate variables, limit the failure domain, check service health, and make rollback explicit.
Script: [Question 145 script](interview-scripts/145-collect-per-host-results-on-localhost.yml)
146. Use `block`, `rescue`, and `always` for cleanup.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
Script: [Question 146 script](interview-scripts/146-use-block-rescue-and-always-for-cleanup.yml)
147. Limit a destructive task to an explicit allow-list.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
Script: [Question 147 script](interview-scripts/147-limit-a-destructive-task-to-an-explicit-allow-list.yml)
148. Convert command output into structured facts.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for Ansible.
Script: [Question 148 script](interview-scripts/148-convert-command-output-into-structured-facts.yml)
149. Test a role under two operating-system families.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
Script: [Question 149 script](interview-scripts/149-test-a-role-under-two-operating-system-families.yml)
150. Build an idempotent deployment playbook with validation, rollback, and audit output.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 150 script](interview-scripts/150-build-an-idempotent-deployment-playbook-with-validation.yml)

## Executable Answers

- [Beginner answers](interview-answers/beginner.yml): idempotent package and service configuration.
- [Intermediate answers](interview-answers/intermediate.yml): rolling deployment, handlers, and health checks.
- [Advanced answers](interview-answers/advanced.yml): health-gated deployment with rescue rollback.
