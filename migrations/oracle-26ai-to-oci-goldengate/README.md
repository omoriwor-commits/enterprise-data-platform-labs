# Oracle 26ai to OCI Migration with GoldenGate 26ai

**Project:** Oracle AI Database 26ai migration from a local Oracle Linux 9.8 lab environment to Oracle Cloud Infrastructure.

## Project distinction

This is a separate project from the [Oracle 19c to 26ai migration on Oracle Linux 7.9 → 9.8](../oracle-19c-to-26ai-goldengate/README.md). The first project combines database modernization and operating-system platform migration. This project concerns **moving an Oracle 26ai workload to OCI** with GoldenGate 26ai.

## Environment summary

| Component | Source | Target |
|---|---|---|
| Platform | Local lab server | Oracle Cloud Infrastructure |
| Operating system | Oracle Linux 9.8 | To confirm from deployment records |
| Oracle database | Oracle AI Database 26ai | Oracle AI Database 26ai |
| Replication technology | Oracle GoldenGate 26ai | Oracle GoldenGate 26ai |
| Initial data movement | Oracle RMAN and Data Pump | Oracle RMAN and Data Pump |
| Hosting model | Local / self-managed | **To confirm: OCI Base Database Service or OCI Compute** |
| Database identifiers | To document | To document |

The OCI target's exact resource type, database service, GoldenGate process layout, IP/VCN configuration and executed steps will be added after checking the implementation records. The title and scope deliberately do not claim an OCI Base Database Service target or a Compute VM without confirmation.

## Architecture record

~~~text
Local Oracle 26ai / Oracle Linux 9.8
                 |
         Oracle GoldenGate 26ai
                 |
       Secure connectivity to OCI
                 |
OCI Oracle 26ai target (hosting type to confirm)
~~~

## Initial load and ongoing replication

The project owner confirms the use of **Oracle RMAN and Oracle Data Pump for initial data loading**, followed by **Oracle GoldenGate 26ai for ongoing change data capture (CDC)**. Replication testing included INSERT, UPDATE, DELETE, and DROP operations. **DROP is DDL**, unlike the three DML operations; its successful replication depends on explicit DDL capture/apply support and configuration. The precise division of work between RMAN and Data Pump, the migration sequence, any backup/restore or export/import parameters, and the SCN/CSN handoff will be documented from the executed commands and logs. Their use is confirmed by the project owner; exact procedures and results are not reconstructed here.

## Implementation evidence to add

- Source and target CDB/PDB details, service names and release identifiers.
- OCI compartment, VCN, subnet, route, security and connectivity design (sanitized).
- GoldenGate deployment and exact Extract/Distribution/Receiver/Replicat topology.
- Applied configuration with secret-free command and parameter examples from the actual environment.
- RMAN commands, backup/restore validation and recovery results as applicable.
- Data Pump export/import commands, job logs, object counts and validation as applicable.
- Baseline instantiation and SCN/CSN coordination with GoldenGate.
- Committed INSERT, UPDATE and DELETE evidence on source and target.
- DROP statement, affected object type, GoldenGate DDL capture/apply settings, and target-side result, to document DDL replication separately.
- Trail/replication checkpoints, lag, restarts, error handling and recovery validation.
- Cutover decision, downtime observations and rollback plan.

## Related engineering references

- [OCI VCN, Public/Private Subnets, Internet and NAT Gateways](https://github.com/omoriwor-commits/DovOps_T/blob/main/OCI/engineering/01-vcn-public-private-subnets-internet-nat-gateways.md)
- [GoldenGate Engineering Field Guide](https://github.com/omoriwor-commits/DovOps_T/blob/main/GoldenGate/manual/README.md)

## Security

Sanitize hostnames, IP addresses, identifiers, logs and topology diagrams where necessary. Never publish cloud account credentials, wallets, passwords, private SSH keys or production application data.
