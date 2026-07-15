# Infrastructure & DevOps Specification: [DEVOPS FEATURE NAME]

**Feature Branch**: `[###-feature-name]`

**Created**: [DATE]

**Status**: Draft

**Input**: User description: "[Brief natural language description of the cloud infrastructure, CI/CD pipeline, or SRE requirements]"

## Operational Journeys & Deployment Testing *(mandatory)*
<!--
  IMPORTANT: Operational journeys represent the workflows, triggers, and deployment targets.
  Each journey must be INDEPENDENTLY VERIFIABLE - meaning if you implement just ONE of them,
  you should still have a viable MVP (Minimum Viable Product) that operates correctly.

  Assign priorities (P1, P2, P3, etc.) to each journey, where P1 is the most critical.
-->

### Operational Journey 1 - [Brief Title] (Priority: P1)
[Describe this cloud provisioning or pipeline journey in plain language]

**Why this priority**: [Explain why this is key to the deployment]

**Independent Verification**: [Describe how this can be tested independently - e.g., "Can be fully verified by running a terraform apply locally and checking resource creation in the console"]

**Acceptance Scenarios**:
1. **Given** [initial environment/state], **When** [trigger/provisioning action], **Then** [expected state/resource behavior]
2. **Given** [initial state], **When** [pipeline execution/deployment trigger], **Then** [expected pipeline outcome/deployment target status]

---

### Operational Journey 2 - [Brief Title] (Priority: P2)
[Describe this alerting, scaling, or recovery journey in plain language]

**Why this priority**: [Explain why this is needed for reliability or security]

**Independent Verification**: [Describe how this can be tested independently - e.g., "Can be verified by simulating a failover event or load testing"]

**Acceptance Scenarios**:
1. **Given** [running environment], **When** [failure/load condition occurs], **Then** [expected self-healing/alerting action]

---

## Infrastructure & Security Requirements *(mandatory)*

### Core Infrastructure Requirements
- **INF-001**: System MUST provision [specific resource type, e.g., "an AWS ECS Cluster using Fargate launch type"]
- **INF-002**: Networking MUST isolate [e.g., "database resources in private subnets with no public internet access"]
- **INF-003**: The provisioning MUST support [e.g., "multi-AZ deployment for RDS to achieve high availability"]

### Security & IAM Requirements
- **SEC-001**: IAM roles MUST enforce [e.g., "least-privilege permissions with explicit resource restrictions"]
- **SEC-002**: Data at rest MUST be [e.g., "encrypted using customer-managed KMS keys"]
- **SEC-003**: Secrets MUST be [e.g., "fetched at runtime from Secret Manager and never committed to version control"]

### Key Cloud Resources
- **[Resource 1]**: [e.g., AWS VPC (10.0.0.0/16, public/private subnets)]
- **[Resource 2]**: [e.g., AWS Aurora PostgreSQL Cluster (v15.4, db.t4g.medium)]

---

## SRE Metrics & Success Criteria *(mandatory)*

### SLO / SLI Targets
- **SRE-001**: **Availability SLO**: Cloud environment uptime must achieve [e.g., "99.9% uptime per month"]
- **SRE-002**: **Deploy Time SLI**: CI/CD pipeline deployment from commit to live must complete in under [e.g., "10 minutes"]
- **SRE-003**: **Error Alerting**: High-priority alerts must trigger if database connection errors exceed [e.g., "1% of connections over 5 minutes"]

### Cost Bounds
- **COST-001**: Non-production environment monthly cost MUST NOT exceed [e.g., "$150/month"]
- **COST-002**: Production infrastructure base cost MUST NOT exceed [e.g., "$800/month"]

---

## Assumptions & Dependencies
- [Assumption about starting state, e.g., "An AWS account with configured root credentials already exists"]
- [Dependency on external providers, e.g., "Domain registration and SSL cert management is hosted in Cloudflare"]
- [Scope boundary, e.g., "Cross-region replication is out of scope for v1"]
