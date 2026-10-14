# Oracle Database 19c to Oracle AI Database 26ai Migration

## Project Overview

I migrated Oracle Database 19c on Oracle Linux 7.9 to Oracle AI Database 26ai on Oracle Linux 9.8.

I used Oracle GoldenGate 26ai for ongoing transactional replication while retaining the Oracle Database 19c Data Guard environment during the migration.

The work covered migration architecture, platform compatibility, change data capture, high availability, validation, troubleshooting, and controlled cutover planning.

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

A key design constraint was operating-system compatibility.

Rather than installing Oracle GoldenGate 26ai directly on the Oracle Linux 7.9 source server, I deployed GoldenGate off-box on the Oracle Linux 9.8 target environment.

The implemented architecture used:

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

This design separated the GoldenGate runtime from the older Oracle Linux 7.9 source platform while retaining access to source redo through remote integrated capture.

It also kept the existing Data Guard configuration independent from the migration replication path.

## Validation Performed

I validated the migration end-to-end in the lab:

- EXT19C registered and capturing from the 19c source (PRODBHR)
- Trail generation and REP26AI apply into PDB23AI
- DML replication: INSERT, UPDATE and DELETE
- DDL replication: CREATE TABLE and DROP TABLE

## Implementation history and engineering decisions

I retained the existing Oracle 19c Data Guard environment and used GoldenGate 26ai from the newer Oracle Linux 9.8 environment to avoid installing the GoldenGate 26ai runtime on the Oracle Linux 7.9 source. My build and troubleshooting notes distinguish source preparation, remote Integrated Extract registration, local trail generation and Integrated Replicat apply from final DML/DDL validation.

## Status

Completed in the lab. Sanitized parameter files and command output will be added after the next rerun.

## Security

Do not commit database passwords, wallet secrets, private SSH keys, cloud credentials, or production data.
