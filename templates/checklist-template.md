# [CHECKLIST TYPE] Checklist: [DEVOPS FEATURE NAME]

**Purpose**: [Brief description of what operational/infrastructure checks this checklist covers]
**Created**: [DATE]
**Feature**: [Link to spec.md or relevant design planning document]

**Note**: This checklist is generated during the checklist phase based on DevOps feature context and requirements.

<!-- 
  ============================================================================
  IMPORTANT: The checklist items below are SAMPLE ITEMS for illustration only.
  
  Replace these with actual items based on:
  - User's specific checklist request (e.g. security audit, cost verification, SRE SLO alerts)
  - Infrastructure requirements from spec.md
  - Network rules from topology.md
  - Validation guidelines from quickstart.md
  - Task status from tasks.md
  
  DO NOT keep these sample items in the generated checklist file.
  ============================================================================
-->

## [Category 1: e.g., Security & IAM Auditing]

- [ ] CHK001 Verify public access block is enabled for all S3 buckets
- [ ] CHK002 Ensure security groups restrict ingress to authorized ports only
- [ ] CHK003 Verify database IAM users enforce least privilege and use Secrets Manager

## [Category 2: e.g., Observability & SRE Alerting]

- [ ] CHK004 Confirm container CPU/Memory alerts route successfully to alerting targets
- [ ] CHK005 Verify application logs include request correlation IDs
- [ ] CHK006 Verify synthetic deployment health checks execute correctly in production

## [Category 3: e.g., Cost & Resource Tags]

- [ ] CHK007 Verify all provisioned resources carry the mandatory environment tags
- [ ] CHK008 Confirm cost alerts trigger if environment budget boundaries are breached

## Notes

- Check items off as completed: `[x]`
- Add verification logs or command output inline
- Link to relevant cloud logs or pipeline run links
- Items are numbered sequentially for easy reference
