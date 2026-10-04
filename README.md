# Enterprise Data Platform Labs

A focused portfolio repository for hands-on enterprise database and data-platform engineering work.

The repository is organized around practical migration, modernization, high-availability, replication, cloud, security, reliability, and automation scenarios.

## Current Lab Portfolio

### Oracle 19c to Oracle AI Database 26ai Migration

[Open the migration lab](migrations/oracle-19c-to-26ai-goldengate/README.md)

Current design:

```text
Oracle Database 19c / Oracle Linux 7.9
        |
        | Remote Integrated Extract
        v
Oracle GoldenGate 26ai
        |
        | Trail
        v
Integrated Replicat
        |
        v
Oracle AI Database 26ai / Oracle Linux 9.8
```

The migration design keeps the existing Oracle 19c Data Guard environment in place while GoldenGate provides continuous change capture toward the 26ai target.

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
    └── oracle-19c-to-26ai-goldengate/
        └── README.md
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
