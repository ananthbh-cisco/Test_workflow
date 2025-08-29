# Architecture Overview

The **Case Management System (CMS)** integrates with PlainID PDP as follows:

1. CMS authenticates users via SSO (outside scope).
2. When a user requests a case:
   - CMS builds an **authorization request** with:
     - `entityId` (user ID)
     - `entityAttributes` (role, region, dept)
     - `resourceAttributes` (case details: region, sensitivity)
     - `environment` (time, IP, device)
3. CMS sends request to **PlainID PDP API**.
4. PDP evaluates policies and returns:
   - `{ "decision": "Permit" }` or `{ "decision": "Deny" }`.
5. CMS enforces decision and logs it.

This repo is not implementing the PDP itself, only documenting **rules and test cases**.
