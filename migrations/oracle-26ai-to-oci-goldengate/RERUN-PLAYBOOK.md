# Local Oracle 26ai → OCI Compute: Migration Rerun Playbook

**Purpose:** Reproduce the completed local Oracle AI Database 26ai → self-managed Oracle 26ai on OCI Compute migration with RMAN, Data Pump and GoldenGate CDC. I used RMAN and Data Pump for initial loading, followed by GoldenGate CDC, and tested INSERT, UPDATE, DELETE and DROP. Original command outputs are not yet archived here.

## Recorded platforms

| Source | Target |
|---|---|
| Local lab / Oracle Linux 9.8 / Oracle 26ai | OCI Compute VM / Oracle Linux 9.8 / self-managed Oracle 26ai |

**Different project:** [Oracle 19c → 26ai and OL7.9 → OL9.8](../oracle-19c-to-26ai-goldengate/README.md). Do not combine their SCN boundaries, Extract processes or validation results.

## Build phases and verification gates

1. **Inventory:** OCI compartment, VCN/subnet/NSG, approved SSH access, Compute shape, volumes and storage; record OS/database/RU versions and source/target CDB/PDB identities.
2. **Connectivity:** Verify source-to-target routes, listeners, SCAN/service naming if applicable, DB connectivity and secure GoldenGate deployment endpoints. Never open TCP 1521 or admin services to the public internet.
3. **Source database readiness:** Check ARCHIVELOG, force logging, supplemental logging, GoldenGate enablement, redo retention, source users and capture privileges appropriate to Oracle 26ai.
4. **Target provisioning:** Install/configure self-managed Oracle 26ai on OCI Compute, correct OS permissions, storage, network and instance-specific target settings.
5. **RMAN path:** Preserve the actual executed backup/restore or duplication method and its recovery requirements. Verify DBID/RESETLOGS, incarnation, PITR/SCN, file-name conversion and CDB/PDB support **before** running recovery commands. Do not assume a source database backup can be restored over a populated target.
6. **Data Pump path:** Preserve actual expdp/impdp mode (FULL/SCHEMAS/TABLES/PDB), directory objects, dump/log location, compatible metadata and remap rules. Confirm imported row counts and failures. Data Pump and RMAN may have served different portions of the migration; do not treat both as interchangeable baseline methods.
7. **CDC boundary:** Establish a consistent initial load and the exact supported Oracle GoldenGate instantiation/CSN boundary for every replicated object; document how RMAN/Data Pump snapshots align with capture and apply.
8. **GoldenGate 26ai:** Record Microservices deployments, credential aliases (never wallet contents), Extract registration/parameters, source/destination trail paths, Distribution/Receiver routes, Replicat parameters and checkpoints. Rebuild from the release-specific docs and verified environment—not assumed old paths.
9. **Test operations:** Execute uniquely keyed committed INSERT, UPDATE, DELETE in a disposable test schema. For DROP, first confirm supported Oracle DDL replication scope, filters and intended test object; verify target metadata and recreate the object as part of controlled teardown.
10. **Operational acceptance:** Reconcile target rows and object definitions, verify checkpoint/lag and restart/catchup, collect error reports, document cutover/rollback and destroy temporary cloud resources when finished.

## Read-only Oracle inventory

Run in the intended container, using an authorized login:

```sql
SELECT banner_full FROM v$version;
SELECT name, database_role, open_mode, log_mode, force_logging FROM v$database;
SELECT con_id, name, open_mode FROM v$pdbs;
SHOW PARAMETER enable_goldengate_replication
SELECT supplemental_log_data_min FROM v$database;
SELECT current_scn FROM v$database;
```

**Important:** The current SCN is an inventory reading, not proof of a Data Pump consistent snapshot or an appropriate Replicat starting CSN. Use an Oracle-supported instantiation workflow.

## Exact commands to collect on rerun

| Phase | Evidence |
|---|---|
| RMAN | Sanitized RMAN script, backup summary, restore/recover report, incarnation/check and DB validation |
| Data Pump | Sanitized parameter files and expdp/impdp logs, object count and error summary |
| Capture | DB logging/privilege checks, Extract configuration/status, trail file sequence and statistics |
| Delivery | Distribution/Receiver config, trail routing and network checkpoints |
| Apply | Replicat config/status, checkpoint and report |
| DML | Before/after SQL on both databases for committed INSERT, UPDATE, DELETE |
| DDL | Supported Oracle DDL settings, DROP statement and resulting target metadata |
| Reliability | Replicat restart, lag trend, missing/duplicate row checks and rollback decision |

Record actual dates, versions and commands. Do not publish data passwords, Oracle wallets, OCI API keys, private SSH keys, account identifiers or customer records.

## Related references

- [Project architecture and recorded methods](README.md)
- [GoldenGate 26ai Engineering Field Guide](https://github.com/omoriwor-commits/oracle-db-platform-automation/blob/main/GoldenGate/manual/README.md)
- [OCI VCN and SSH Engineering Guide](https://github.com/omoriwor-commits/oracle-db-platform-automation/blob/main/OCI/engineering/README.md)
- [Oracle GoldenGate 26ai core documentation](https://docs.oracle.com/en/database/goldengate/core/26/coredoc/index.html)
