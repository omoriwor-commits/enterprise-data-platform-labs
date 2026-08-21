# Oracle Database 19c to Oracle AI Database 26ai Migration

## Project Overview

This project implements and validates a database modernization path from Oracle Database 19c on Oracle Linux 7.9 to Oracle AI Database 26ai on Oracle Linux 9.8.

The migration architecture uses Oracle GoldenGate 26ai for ongoing transactional replication while maintaining the existing Oracle Database 19c Data Guard environment during the migration.

The project focuses on migration architecture, platform compatibility, change data capture, high availability, validation, troubleshooting, and controlled cutover planning.

---

## Objectives

- Migrate from Oracle Database 19c to Oracle AI Database 26ai
- Move from Oracle Linux 7.9 to Oracle Linux 9.8
- Maintain the existing Oracle 19c Data Guard environment during migration
- Minimize application downtime
- Use a supported Oracle GoldenGate architecture
- Establish continuous change data capture between source and target
- Validate source-to-target transactional replication
- Maintain a documented cutover and rollback strategy

---

## Source Environment

- Oracle Database 19c
- Oracle Linux 7.9
- Multitenant architecture
- Source PDB: `PRODBHR`
- Oracle Data Guard
  - Primary database
  - Physical standby database

---

## Target Environment

- Oracle Linux 9.8
- Oracle AI Database 26ai Enterprise Edition
- Multitenant architecture
- Target PDB: `PDB23AI`
- Oracle GoldenGate 26ai Microservices

---

## Architecture Decision

A key design constraint was operating-system compatibility.

Rather than installing Oracle GoldenGate 26ai directly on the Oracle Linux 7.9 source server, GoldenGate was deployed off-box on the Oracle Linux 9.8 target environment.

The selected architecture uses:

- Remote Integrated Extract for source capture
- Local GoldenGate trail
- Integrated Replicat for target apply

### Replication Flow

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
