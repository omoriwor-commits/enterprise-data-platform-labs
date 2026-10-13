# Oracle 26ai to OCI Migration with GoldenGate 26ai

**Project:** Oracle AI Database 26ai migration from a local Oracle Linux 9.8 lab environment to Oracle Cloud Infrastructure.

[**Repeat the implementation: RMAN, Data Pump and GoldenGate rerun playbook**](RERUN-PLAYBOOK.md)

## Project distinction

This is a separate project from the [Oracle 19c to 26ai migration on Oracle Linux 7.9 → 9.8](../oracle-19c-to-26ai-goldengate/README.md). The first project combines database modernization and operating-system platform migration. This project concerns **moving an Oracle 26ai workload to OCI** with GoldenGate 26ai.

## Environment summary

| Component | Source | Target |
|---|---|---|
| Platform | Local lab server | Oracle Cloud Infrastructure |
| Operating system | Oracle Linux 9.8 | Oracle Linux 9.8 |
| Oracle database | Oracle AI Database 26ai | Oracle AI Database 26ai |
| Replication technology | Oracle GoldenGate 26ai | Oracle GoldenGate 26ai |
| Initial data movement | Oracle RMAN and Data Pump | Oracle RMAN and Data Pump |
| Hosting model | Local / self-managed | **OCI Compute VM, self-managed Oracle 26ai** |

The OCI target was an **OCI Compute virtual machine with Oracle AI Database 26ai installed and administered directly**, not OCI Base Database Service. Exact VM shape, database identifiers, network topology, GoldenGate process layout and executed commands should be documented from implementation records.

## Architecture record

~~~text
Local Oracle 26ai / Oracle Linux 9.8
                 |
         Oracle GoldenGate 26ai
                 |
       Secure connectivity to OCI
                 |
OCI Compute VM / Oracle Linux 9.8
Self-managed Oracle AI Database 26ai
~~~

## Initial load and ongoing replication

I used **Oracle RMAN and Data Pump for initial data loading**, followed by **GoldenGate 26ai for ongoing CDC**. I tested INSERT, UPDATE, DELETE and DROP operations. The rerun playbook records the validation sequence and the commands and outputs to capture on the next execution.

## Related engineering references

- [OCI VCN, Public/Private Subnets, Internet and NAT Gateways](https://github.com/omoriwor-commits/DovOps_T/blob/main/OCI/engineering/01-vcn-public-private-subnets-internet-nat-gateways.md)
- [GoldenGate Engineering Field Guide](https://github.com/omoriwor-commits/DovOps_T/blob/main/GoldenGate/manual/README.md)

## Security

Sanitize hostnames, IP addresses, identifiers, logs and topology diagrams where necessary. Never publish cloud account credentials, wallets, passwords, private SSH keys or production application data.
