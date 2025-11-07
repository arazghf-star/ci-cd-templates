# Security Policy

## Supported Versions

This project contains reusable CI/CD workflow templates. Security updates are applied to the latest versions.

| Version | Supported          |
| ------- | ------------------ |
| Latest  | :white_check_mark: |

## Reporting a Vulnerability

If you discover a security vulnerability in these CI/CD templates, please report it by:

1. **DO NOT** open a public issue
2. Email: araz.ghf@gmail.com with subject "Security: CI/CD Templates"
3. Include:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)

We will respond within 48 hours and work on a fix promptly.

## Security Best Practices

These workflow templates implement several security best practices:

### 1. Minimal Permissions
- Use `permissions:` block to grant least-privilege access
- Prefer `contents: read` over `contents: write`
- Use `id-token: write` only when needed for OIDC

### 2. Dependency Pinning
- Pin GitHub Actions to full commit SHA
- Use Dependabot to keep actions updated
- Review action updates before merging

### 3. Secret Management
- Never hardcode secrets in workflows
- Use GitHub Secrets for sensitive data
- Rotate secrets regularly
- Use OIDC federation instead of long-lived credentials where possible

### 4. Security Scanning
- Trivy for container and IaC scanning
- tfsec for Terraform security checks
- Gitleaks for secret detection
- SARIF upload to GitHub Security tab

### 5. Artifact Security
- Use short retention periods for artifacts
- Scan artifacts before use
- Never upload secrets as artifacts

### 6. Branch Protection
Recommended branch protection rules:
- Require pull request reviews
- Require status checks to pass
- Require branches to be up to date
- Include administrators in restrictions

## Security Features in Templates

### Python Test Workflow
- Dependency caching with hash verification
- No arbitrary code execution
- Read-only permissions

### Docker Build & Scan
- Multi-stage builds to reduce attack surface
- Trivy vulnerability scanning
- SARIF results uploaded to Security tab
- Non-root user enforcement
- Image signing (optional)

### Terraform Validate
- tfsec security scanning
- Checkov policy checks
- No AWS credentials in workflows (use OIDC)
- Validation only, no apply in CI

### Security Scan Workflow
- Comprehensive scanning (Trivy, Gitleaks, Bandit)
- SARIF format for GitHub integration
- Fail on high severity findings
- SBOM generation

### Helm Deploy to kind
- Ephemeral test clusters only
- No production deployments
- Policy validation with OPA
- Kubeconform schema validation

## Known Limitations

1. **LocalStack Only**: Production AWS credentials should never be used in these workflows
2. **kind Clusters**: Suitable for testing only, not production
3. **Public Workflows**: Ensure no secrets in workflow files themselves

## Third-Party Actions

We use the following trusted third-party actions:

- `actions/checkout@v4` - Official GitHub action
- `actions/setup-python@v5` - Official GitHub action
- `docker/build-push-action@v5` - Official Docker action
- `aquasecurity/trivy-action@master` - Maintained by Aqua Security
- `hashicorp/setup-terraform@v3` - Official HashiCorp action

All actions are reviewed before use and updated regularly.

## Compliance

These workflows are designed to support:

- SOC 2 compliance (audit trails, security scanning)
- ISO 27001 (access control, change management)
- GDPR (no PII in logs or artifacts)
- HIPAA (encrypted secrets, audit logs)

## Security Checklist for Users

When using these templates:

- [ ] Review the workflow before enabling
- [ ] Configure required secrets
- [ ] Set up branch protection rules
- [ ] Enable Dependabot alerts
- [ ] Enable secret scanning
- [ ] Enable code scanning (CodeQL)
- [ ] Configure CODEOWNERS file
- [ ] Set up security policy
- [ ] Regular security audits
- [ ] Monitor security advisories

## Questions?

For security-related questions, email: araz.ghf@gmail.com

For general questions, open a GitHub Discussion (not an Issue).

---

**Last Updated:** 2024-11-07
