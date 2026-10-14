# Enterprise Data Platform Labs

A focused portfolio repository for hands-on enterprise database and data-platform engineering work.

The repository is organized around practical migration, modernization, high-availability, replication, cloud, security, reliability, and automation scenarios.

## Current Lab Portfolio

These are migrations 1 and 2 of a three-stage path; migration 3 (OCI → Azure SQL Server 2022) is in the enterprise-multicloud-database-platform-lab repository.
### Migration 1 — Oracle Database Upgrade, OS Migration & GoldenGate Replication — remote capture / local apply

[Open the migration lab](migrations/oracle-19c-to-26ai-goldengate/README.md)

Current design:

```text
Oracle Database 19c / Oracle Linux 7.9
        |
        | Oracle Net: REMOTE Integrated Extract EXT19C
        v
GoldenGate 26ai on OL9.8 TARGET host
        | Integrated Replicat REP26AI: LOCAL apply
        v
Oracle AI Database 26ai / Oracle Linux 9.8
```

The migration design keeps the existing Oracle 19c Data Guard environment in place while GoldenGate provides continuous change capture toward the 26ai target.

### Migration 2 — Oracle On-Premises to OCI Cloud Migration & GoldenGate Replication — local capture / remote apply

[Open the OCI migration](migrations/oracle-26ai-to-oci-goldengate/README.md)

```text
LOCAL / OL9.8                                 OCI COMPUTE / OL9.8
Oracle AI Database 26ai                       Oracle AI Database 26ai
GoldenGate source-side tier                   (self-managed target)
   Extract: LOCAL capture                         ^
   Replicat: REMOTE apply ------------------------+
Initial load: RMAN + Data Pump; CDC: GoldenGate 26ai
```

The [OCI-to-Azure SQL Server 2022 project](https://github.com/omoriwor-commits/enterprise-multicloud-database-platform-lab) is migration 3: a hub-based **remote capture / remote apply** heterogeneous migration.

## Focus Areas

- Oracle Database engineering
- database migration and modernization
- GoldenGate replication and CDC
- Data Guard / HA-DR
- multitenant architecture
- RMAN and recovery
- cloud database platforms
- security and governance
- performance and reliability engineering
- automation
- enterprise data-platform architecture

## Technologies

### Database

- Oracle Database 19c
- Oracle AI Database 26ai
- Oracle Multitenant (CDB/PDB)
- RMAN
- Data Pump
- Data Guard
- Oracle GoldenGate

### Cloud

- Oracle Cloud Infrastructure (OCI)
- Microsoft Azure
- Amazon Web Services (AWS)

### Infrastructure

- Oracle Linux
- Red Hat Enterprise Linux
- Linux administration
- networking
- storage

## Repository Structure

```text
enterprise-data-platform-labs/
├── README.md
└── migrations/
    ├── README.md
    ├── oracle-19c-to-26ai-goldengate/
    │   └── README.md
    └── oracle-26ai-to-oci-goldengate/
        ├── README.md
        └── RERUN-PLAYBOOK.md
```

The structure will expand only as new labs are actually added. This avoids empty placeholder directories and keeps the repository aligned with completed or active work.

## Documentation Standard

Each lab should document:

1. Objective
2. Source environment
3. Target environment
4. Architecture
5. Prerequisites
6. Implementation steps
7. Validation
8. Troubleshooting
9. Cutover / rollback considerations
10. Lessons learned

## Related Portfolio Repositories

- [Enterprise Multi-Cloud Database Platform Lab](https://github.com/omoriwor-commits/enterprise-multicloud-database-platform-lab)
- [Nginx DevOps Assignment](https://github.com/omoriwor-commits/nginx-devops-assignment)

## Security

Do not commit passwords, private keys, database wallet secrets, cloud credentials, access tokens, or production data.
