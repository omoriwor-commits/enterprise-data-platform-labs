# Oracle Database 19c to Oracle AI Database 26ai Migration

## Project Overview

This lab documents a database modernization design from Oracle Database 19c on Oracle Linux 7.9 to Oracle AI Database 26ai on Oracle Linux 9.8.

Oracle GoldenGate 26ai is used for ongoing transactional replication while the existing Oracle Database 19c Data Guard environment remains in place during the migration.

The lab focuses on migration architecture, platform compatibility, change data capture, high availability, validation, troubleshooting, and controlled cutover planning.

## Objectives

- Migrate from Oracle Database 19c to Oracle AI Database 26ai.
- Move from Oracle Linux 7.9 to Oracle Linux 9.8.
- Maintain the existing Oracle 19c Data Guard environment during migration.
- Minimize application downtime.
- Use a supported GoldenGate architecture.
- Establish continuous change data capture between source and target.
- Validate source-to-target transactional replication.
- Define cutover and rollback considerations.

## Source Environment

| Component | Value |
|---|---|
| Database | Oracle Database 19c |
| Operating system | Oracle Linux 7.9 |
| Architecture | Multitenant |
| Source PDB | `PRODBHR` |
| HA/DR | Oracle Data Guard |

The source environment includes a primary database and a physical standby database.

## Target Environment

| Component | Value |
|---|---|
| Operating system | Oracle Linux 9.8 |
| Database | Oracle AI Database 26ai Enterprise Edition |
| Architecture | Multitenant |
| Target PDB | `PDB23AI` |
| Replication | Oracle GoldenGate 26ai Microservices |

## Architecture Decision

A key design constraint is operating-system compatibility.

Rather than installing Oracle GoldenGate 26ai directly on the Oracle Linux 7.9 source server, GoldenGate is deployed off-box on the Oracle Linux 9.8 target environment.

The selected architecture uses:

- Remote Integrated Extract for source capture
- local GoldenGate trail
- Integrated Replicat for target apply

## Replication Flow

```text
Oracle Database 19c / PRODBHR
        |
        v
Remote Integrated Extract
EXT19C
        |
        v
GoldenGate Trail
        |
        v
Integrated Replicat
REP26AI
        |
        v
Oracle AI Database 26ai / PDB23AI
```

## Design Rationale

This design separates the GoldenGate runtime from the older Oracle Linux 7.9 source platform while retaining access to source redo through remote integrated capture.

It also keeps the existing Data Guard configuration independent from the migration replication path.

## Planned Validation

The lab should validate:

- Extract registration and startup
- source transaction capture
- trail generation
- Replicat startup
- target apply
- INSERT, UPDATE, and DELETE replication
- source/target row reconciliation
- replication lag
- restart/checkpoint behavior
- cutover readiness
- rollback path

## Status

**Active / in progress.**

The repository currently documents the architecture and migration design. Implementation evidence and validation results should be added only as each stage is completed.

## Next Documentation Additions

- prerequisites and compatibility checks
- source database preparation
- GoldenGate deployment steps
- Extract configuration
- Replicat configuration
- validation evidence
- troubleshooting record
- cutover runbook
- rollback runbook

## Security

Do not commit database passwords, wallet secrets, private SSH keys, cloud credentials, or production data.
