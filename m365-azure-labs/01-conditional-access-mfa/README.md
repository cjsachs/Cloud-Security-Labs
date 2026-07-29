# Lab 01: Conditional Access - Require MFA for All Users

## Objective
Deploy a Conditional Access policy enforcing MFA across all users in a
sandboxed Microsoft 365 E3 tenant, following a safe test-before-enforce
workflow. Supports M365/Azure Administrator cert prep and AZ-104 study.

## What I Built
- Created `CA001 - Require MFA for All Users` targeting all users
  (admin account excluded to prevent lockout during testing) and all
  cloud apps
- Deployed initially in **Report-only** mode to validate impact before
  enforcing
- Created a test user (`christiantest@duganlab.onmicrosoft.com`) to
  generate sign-in events for validation

## Troubleshooting
Policy showed "Not applied" on all sign-in events despite being correctly
configured. Root cause turned out to be a **Security Defaults conflict**:
Security Defaults and custom Conditional Access policies cannot run
together, so the tenant wasn't evaluating CA001 at all.

Disabling Security Defaults triggered Entra to auto-generate four
Microsoft-managed baseline CA policies as a replacement (Block legacy
authentication, MFA for Azure Management, MFA for admins, MFA for all
users) — a newer platform behavior rather than something manually
configured.

After disabling Security Defaults and allowing time for propagation,
validated CA001 was being evaluated and returning **Success** by
checking the **Conditional Access** tab on individual sign-in log
entries (not just the summary column, which can lag).

## Validation
- Confirmed via Entra admin center → Monitoring & health → Sign-in
  events → clicked into a specific `christiantest` sign-in → Conditional
  Access tab → CA001 listed with result: Success
- Flipped policy from Report-only to **On** (enforced) after validation

## Screenshots
![Policy configuration](m365-azure-labs\01-conditional-access-mfa\screenshots\policy config.png)
![Sign-in log showing policy applied](m365-azure-labs/01-conditional-access-mfa/screenshots/Sign-in log showing policy applied.png)

## Key Takeaway
Report-only mode plus sign-in log validation is the safe way to test
Conditional Access policies before enforcing, preventing accidental
lockouts in production. Also confirmed that a policy "existing" and a
policy "evaluating" are two different things worth checking separately,
especially in a tenant where Security Defaults may still be active.