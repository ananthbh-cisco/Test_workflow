# PlainID Access Control Testing

This repository defines business rules and test cases for **PlainID Policy Decision Point (PDP)** integration.

## What is PlainID PDP?
PlainID provides **Policy-Based Access Control (PBAC)**.  
The **Policy Decision Point (PDP)** evaluates user, resource, and environment attributes and returns an **authorization decision**:
- **Permit** → User is allowed access.
- **Deny** → User is not allowed access.

## Project Goal
We want to:
1. Document the business rules for when PDP should return **Permit** vs **Deny**.
2. Provide sample requests/responses in JSON format.
3. Define test cases so GitHub Copilot can generate:
   - Unit tests
   - Integration tests
   - BDD feature files
   - Postman test collections

## Example Flow
1. CMS calls PlainID PDP API with:
   - `entityAttributes` (role, region, department)
   - `resourceAttributes` (region, sensitive flag)
   - `environment` (time, IP, device)
2. PDP applies business rules.
3. PDP returns `{ "decision": "Permit" }` or `{ "decision": "Deny" }`.

## Key Rules
- Admins can access all cases (unless outside working hours).
- Managers can only access cases in their region, and not sensitive ones.
- Agents can access only non-sensitive cases in their region.
- Guests/Unknown roles are always denied.
- Access is restricted outside **08:00–20:00** local time.
- System errors, malformed requests, or timeouts → **Deny**.

For detailed rules, see:
- [BRD.md](./docs/BRD.md)
- [DECISION_MATRIX.md](./docs/DECISION_MATRIX.md)
- [TEST_CASES.md](./tests/TEST_CASES.md)
