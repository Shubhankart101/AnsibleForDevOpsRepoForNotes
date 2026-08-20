# AWS Ansible Use Cases

## 1. AWS account and network automation

- Use `amazon.aws` modules to manage VPCs, subnets, route tables, security groups, IAM roles, and shared services.
- Separate accounts and environments with inventories, reusable roles, tags, and controlled execution identities.
- Use short-lived credentials through OIDC or an approved secret-management integration.

## 2. Application platform delivery

- Automate EC2, Auto Scaling, load balancers, ECS services, and supporting configuration with idempotent playbooks.
- Build immutable application releases while keeping host bootstrap and operational configuration repeatable.
- Run syntax checks, linting, check mode, and integration tests in CI before promotion.

## 3. Operations and compliance

- Automate patch baselines, SSM configuration, CloudWatch agents, service validation, and certificate renewal.
- Enforce tagging, least privilege, hardened host settings, and account guardrails through reusable roles.
- Export execution results for audit and incident timelines.

## 4. Reliability and recovery

- Coordinate multi-AZ rollout, health checks, backup validation, restore workflows, and controlled rollback.
- Exercise disaster recovery playbooks against documented RTO and RPO targets.
