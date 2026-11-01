# Incident Response Plan

## 1. Purpose
Define how security incidents affecting our cloud infrastructure and source code are detected, contained, eradicated and recovered from.

## 2. Scope
GitHub repositories, AWS account (IAM, S3), Terraform Cloud workspace T-lab-org/T-AWS-lab.

## 3. Roles
| Role | Responsibility |
|------|----------------|
| Incident Commander | Declares the incident, makes containment decisions |
| Security Analyst | Investigates logs (CloudTrail, GitHub Actions) |
| Infrastructure Engineer | Rotates credentials, updates Terraform Cloud, restores service |

## 4. Severity Levels
| Level | Definition | Example |
|-------|------------|---------|
| Low | No exposure of credentials or data | Failed scan on test code |
| Medium | Credential exposed, no evidence of use | Key committed to a repo |
| High | Evidence of unauthorized use or data access | Unknown IP calling S3 APIs |
| Critical | Confirmed data exfiltration or destruction | Bucket contents downloaded/deleted |

## 5. Response Phases
1. **Detection and Analysis** - confirm alert, identify what was exposed, check logs for misuse, assign severity.
2. **Containment** - deactivate the exposed credential immediately.
3. **Eradication** - delete the credential, remove the secret from the codebase.
4. **Recovery** - issue new credentials, update Terraform Cloud, verify infrastructure.
5. **Post-Incident** - write incident report, add preventive controls, update this plan.

## 6. Preventive Controls
- Gitleaks secret scanning on every push (GitHub Actions)
- Bandit (code), Checkov (IaC), Trivy (containers), OWASP ZAP (web app) in CI
- S3 hardening: public access block, KMS encryption, versioning, logging
- Sensitive variables in Terraform Cloud; never credentials in code
