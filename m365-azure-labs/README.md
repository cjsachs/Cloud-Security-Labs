# M365 & Azure Administration Labs

Built in a sandboxed Microsoft 365 E3 trial tenant (`duganlab.onmicrosoft.com`)
to develop hands-on Entra ID / M365 admin experience beyond what's safely
testable in a live production environment.

## Labs

| # | Lab | Status | Summary |
|---|-----|--------|---------|
| 01 | [Conditional Access - Require MFA](./01-conditional-access-mfa/README.md) | Complete | Deployed and validated a CA policy enforcing MFA for all users |
| 02 | [Dynamic Security Groups](./02-dynamic-security-groups/README.md) | Complete | Built a Dynamic User group with department-based membership rule |

More labs will be added here as they're completed (legacy auth blocking,
Intune compliance, Azure infrastructure).

## Environment Setup Notes
- Tenant: Microsoft 365 E3 trial (30-day, recurring billing disabled)
- 10 test users created via CSV bulk import across 4 departments
  (Sales, IT, Finance, Marketing) to support group/policy testing
- Security Defaults disabled early on; Entra auto-generated 4 baseline
  Conditional Access policies to replace it (worth knowing, this
  is a newer default behavior, not something you configure manually)