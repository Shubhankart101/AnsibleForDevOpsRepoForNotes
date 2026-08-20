# Ansible Interview Question Bank

This bank contains 120 questions organized by difficulty. Use the numbered scripts in `scripts/` to build answers with working examples.

## Beginner: 1-40

1. What problem does Ansible solve?
2. How does Ansible differ from agent-based configuration tools?
3. What is an Ansible inventory?
4. What is the difference between a host and a group?
5. What is a playbook?
6. What is a play?
7. What is a task?
8. What is a module?
9. What is a fully qualified collection name?
10. What does idempotence mean in Ansible?
11. Why should `ansible.builtin.command` be used carefully?
12. When would you use the `shell` module?
13. What does `ansible.builtin.ping` actually verify?
14. How do you run a playbook in check mode?
15. What does `--diff` show?
16. How do you pass an extra variable at runtime?
17. What is the difference between `vars` and `vars_files`?
18. How do you use a variable in a task?
19. What is a loop and how is it written?
20. How do you register task output?
21. What is a handler?
22. When does a handler run?
23. How do you notify a handler?
24. How do `when` conditions work?
25. How do you install a package portably?
26. How do you manage a service?
27. How do you create a user with Ansible?
28. How do you copy a static file?
29. When should you use `template` instead of `copy`?
30. What is privilege escalation with `become`?
31. How do you limit execution to selected hosts?
32. What does `gather_facts` do?
33. How do you print a variable for troubleshooting?
34. How do you use tags?
35. What is YAML indentation significance?
36. How do you check playbook syntax?
37. What is the difference between a changed and failed task?
38. How do you make a command task report no change?
39. What is an Ansible role?
40. What information belongs in an inventory file?

## Intermediate: 41-80

41. Explain Ansible variable precedence with an example.
42. How do role defaults differ from role vars?
43. What belongs in `tasks`, `handlers`, `templates`, and `defaults`?
44. How do you design a reusable role?
45. How do role dependencies work?
46. How do you use `include_tasks` and `import_tasks`?
47. When should you use a dynamic include?
48. How do you loop over a block of tasks?
49. How do you combine registered results from a loop?
50. How do you use `changed_when` correctly?
51. How do you use `failed_when` safely?
52. Explain `block`, `rescue`, and `always`.
53. How do you implement rollback after a failed deployment?
54. What does `serial` do during a rolling deployment?
55. How do `max_fail_percentage` and `any_errors_fatal` differ?
56. What is the difference between `linear` and `free` strategy?
57. How do you delegate a task to localhost?
58. How do you share facts between hosts?
59. How do you run long jobs asynchronously?
60. How do you poll an asynchronous job?
61. How does `run_once` affect a task?
62. How do you validate a rendered configuration before replacing it?
63. How do you use `assert` to validate inputs?
64. How do you wait for a service or port?
65. How do you perform an HTTP health check?
66. How do you find files older than a retention period?
67. How do you safely remove old releases?
68. How do you manage line-based configuration?
69. How do you preserve secrets with Ansible Vault?
70. How should Vault passwords be supplied in CI?
71. What is a lookup plugin?
72. What is a filter plugin?
73. How do you transform data with Jinja filters?
74. How do you use `set_fact` without creating confusing state?
75. How do you pass environment variables to a task?
76. How do you use check mode in custom commands?
77. How do you test a role with Molecule?
78. How do Ansible lint and syntax check differ?
79. How do you troubleshoot an unreachable host?
80. How do you design inventories for dev, test, and production?

## Advanced: 81-120

81. How would you design Ansible for a multi-account Azure estate?
82. How would you design Ansible for multiple AWS accounts and regions?
83. How do dynamic inventory plugins discover cloud hosts?
84. How do you authenticate to Azure without long-lived secrets?
85. How do you authenticate to AWS through an assumed role?
86. How do you enforce cloud resource tags with Ansible?
87. How do you make a cloud provisioning playbook safe to rerun?
88. How do you handle eventual consistency in cloud APIs?
89. How do you implement blue-green deployment with Ansible?
90. How do you implement canary deployment with `serial`?
91. How would you gate rollout on SLO or health data?
92. How would you design a safe rollback when database schema changes?
93. How do you coordinate application and infrastructure changes?
94. How do you prevent two production playbooks running concurrently?
95. How do you expose structured audit events from automation?
96. How do you redact secrets from logs and callback output?
97. How do you secure self-hosted Ansible execution nodes?
98. How do you separate controller, execution environment, and target trust?
99. What are Ansible execution environments?
100. How do you pin collection and Python dependencies?
101. How do you manage collections in a reproducible build?
102. How do you design an Ansible CI pipeline?
103. Which quality gates belong before production execution?
104. How do you use Molecule with container and VM drivers?
105. How do you test idempotence automatically?
106. How do you test a role across operating-system families?
107. How do you handle Windows and Linux targets in one platform?
108. How do you manage VMware or Hyper-V with Ansible?
109. How do you automate hybrid on-premises and cloud connectivity?
110. How do you design patch orchestration for a large fleet?
111. How do you avoid a patch rollout becoming a fleet-wide outage?
112. How do you implement certificate expiry monitoring?
113. How do you validate backups and restores with Ansible?
114. How do you automate disaster-recovery exercises?
115. How do you measure automation success and change failure rate?
116. How do you investigate drift between desired and actual state?
117. How do you handle partial failure across many hosts?
118. How do you design recovery when the Ansible controller is unavailable?
119. What are the main risks of using `command` and `shell` in production?
120. Design an end-to-end Ansible platform for secure, observable, reversible delivery.

## HackerRank-Style Automation Challenges: 121-150

121. Write a playbook that creates a user only when it is absent.
122. Write a playbook that installs packages from a variable list and reports failures.
123. Write a role that renders a service config and restarts only when content changes.
124. Write a playbook that parses a JSON API response and asserts a required field.
125. Write a playbook that retries an HTTP health check with a bounded delay.
126. Write a playbook that finds files older than 30 days and deletes them in check mode first.
127. Write a playbook that compares desired ports with firewall rules and reports drift.
128. Write a playbook that processes hosts in batches of two.
129. Write a playbook that rolls back a release when a health task fails.
130. Write a playbook that runs a long command asynchronously and polls its job ID.
131. Write a custom filter that converts host objects into a name-to-IP map.
132. Write a role test that proves a second run produces no changes.
133. Validate required variables before any remote task runs.
134. Write an audit event with change ID and inventory host.
135. Safely handle a missing optional file.
136. Use a vaulted password without exposing it in output.
137. Group dynamic inventory instances by environment tag.
138. Ensure an Azure resource group has required tags.
139. Discover AWS instances and verify their security group.
140. Fail deployment when a certificate has fewer than 14 days remaining.
141. Validate backup size and timestamp.
142. Restore the previous release from a symlink.
143. Execute a database migration exactly once.
144. Skip production changes unless an approval variable is true.
145. Collect per-host results on localhost.
146. Use `block`, `rescue`, and `always` for cleanup.
147. Limit a destructive task to an explicit allow-list.
148. Convert command output into structured facts.
149. Test a role under two operating-system families.
150. Build an idempotent deployment playbook with validation, rollback, and audit output.
