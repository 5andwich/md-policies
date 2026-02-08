# FedRAMP KSI Access Management Policy Pack

This folder provides a machine-readable and human-readable policy set for **FedRAMP KSI access management** controls. The design is modular so additional FedRAMP control families (for example AU, CM, IR, SC) can be added without changing the core model.

## Structure

- `policy-set.json`: entrypoint manifest for this control family.
- `AM-001` to `AM-005` JSON files: machine-readable policy units.
- `../../../schema/policy.schema.json`: shared schema that standardizes policy format across all control families.

## Policy catalog

| Policy ID | Title | FedRAMP Mapping | Intent |
|---|---|---|---|
| FEDRAMP-KSI-AM-001 | Identity and Account Lifecycle Management | AC-2, IA-4 | Enforce approved provisioning and timely deprovisioning. |
| FEDRAMP-KSI-AM-002 | Least Privilege and Role-Based Access Enforcement | AC-6, AC-3 | Restrict access to approved role-based permissions. |
| FEDRAMP-KSI-AM-003 | Multi-Factor Authentication Coverage | IA-2, IA-2(1), IA-2(2) | Require MFA, with strongest controls for privileged access. |
| FEDRAMP-KSI-AM-004 | Privileged Access Management and Session Control | AC-5, AC-6(10), AU-12 | Govern privileged elevation and ensure accountability. |
| FEDRAMP-KSI-AM-005 | Periodic Access Certification | AC-2(7), AC-2(12), CA-7 | Continuously verify access remains appropriate. |

## How this scales to other compliance controls

1. Copy the same folder pattern: `policies/fedramp/ksi/<control-family>/`.
2. Reuse `policy.schema.json` for each policy file in that family.
3. Create a family-level `policy-set.json` manifest with references to each policy file.
4. Keep mappings in `control_mappings` so one policy can satisfy multiple compliance controls.
5. Add automation expressions in `policy_logic.conditions` to support continuous control monitoring.

## Suggested implementation workflow

1. Validate JSON file structure against the shared schema.
2. Build parser/engine adapters for your IAM, IdP, PAM, and SIEM tools.
3. Evaluate each `policy_logic.conditions[*].expression` on a scheduled cadence.
4. Trigger `policy_logic.actions` automatically when conditions fail.
5. Archive `evidence_requirements` outputs for audit readiness.
