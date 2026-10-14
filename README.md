# Enterprise Data Platform Labs

A focused portfolio repository for hands-on enterprise database and data-platform engineering work.

The repository is organized around practical migration, modernization, high-availability, replication, cloud, security, reliability, and automation scenarios.

## Current Lab Portfolio

These are migrations 1 and 2 of a three-stage path; migration 3 (OCI → Azure SQL Server 2022) is in the enterprise-multicloud-database-platform-lab repository.

### Migration 1 — Oracle 19c → 26ai Upgrade, OS Migration & GoldenGate Replication

[Open the migration lab](migrations/oracle-19c-to-26ai-goldengate/README.md)

Architecture:

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

I kept the existing Oracle 19c Data Guard environment in place while GoldenGate provided continuous change capture to the 26ai target.

### Migration 2 — Oracle 26ai On-Premises to OCI Migration & GoldenGate Replication

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

- Oracle database migration and upgrade
- GoldenGate replication and CDC
- RMAN and Data Pump initial loads
- Oracle Data Guard
- Oracle Cloud Infrastructure (OCI)

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

### Infrastructure

- Oracle Linux
- Linux administration

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

## Related Portfolio Repositories

- [Enterprise Multi-Cloud Database Platform Lab](https://github.com/omoriwor-commits/enterprise-multicloud-database-platform-lab)
- [Nginx DevOps Project](https://github.com/omoriwor-commits/nginx-devops-project)

