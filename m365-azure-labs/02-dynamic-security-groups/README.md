# Lab 02: Dynamic Security Groups

## Objective
Build a Dynamic User security group in Entra ID that automatically
maintains membership based on a user attribute, rather than manually
assigning members. Supports M365/Azure Administrator cert prep.

## What I Built
- Created 10 test users via bulk CSV import across 4 departments
  (Sales, IT, Finance, Marketing) to have real data to query against
- Created `DYN-Sales-Users`, a Security group with **Dynamic User**
  membership type
- Wrote a dynamic membership rule using rule syntax:
  ```
  (user.department -eq "Sales")
  ```
- Used the **Validate Rules** preview to confirm the rule matched the
  correct users before saving
- Saved the group and confirmed all 3 Sales department users
  (Sarah Chen, Mike Torres, Jenny Kim) were added automatically

## Validation
- Checked the group's **Members** tab in Entra admin center
- Confirmed all 3 Sales users populated without manual assignment

## Screenshots
![Dynamic rule syntax/builder](02-dynamic-security-groups\screenshots\dynamic rule syntax.png)
![Group membership populated](02-dynamic-security-groups\screenshots\sales members.png)

## Key Takeaway
Dynamic groups remove the manual overhead of adding/removing users as
department or role changes, membership stays accurate automatically
based on directory attributes. This is the kind of automation that
scales; assigned groups work fine for 10 users, but become an
operational burden at the size of a real org. Validating the rule
before saving is worth doing every time, since a bad rule syntax can
silently return zero matches or the wrong population.