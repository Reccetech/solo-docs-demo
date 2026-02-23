---
title: 'Using "Task" and Examples'
weight: 180
description: >
  Use Task to launch Solo quickly, then explore GitHub example projects.
type: docs
---

## Use the Task tool to Launch Solo

For developers who want to quickly deploy a standalone Hiero Consensus Node network without needing to know what is under the hood, they can use the Task tool to launch the network with a single command.

NOTE: this requires cloning the GitHub repository: <https://github.com/hiero-ledger/solo>

First, install the cluster tool `kind` with this [link](https://kind.sigs.k8s.io/docs/user/quick-start#installation).

Then, install the task tool `task` with this [link](https://taskfile.dev/installation/).

`task` will install dependencies and build the Solo project.

### Start the Hiero Consensus Node network

You can use one of the following three commands to quickly deploy a standalone Hiero Consensus Node network:

```bash
# Option 1) Deploy the network with two nodes. `task` is the same as `task default`.
task

# Option 2) Deploy the network with two nodes and a Mirror Node.
cd scripts
task default-with-mirror

# Option 3) Deploy the network with two nodes, a Mirror Node, and a JSON RPC Relay.
cd scripts
task default-with-relay
```

If a Mirror Node or a Relay node is deployed, you can access the Hiero Explorer at <http://localhost:8080>.

### Stop the Consensus Node network

To tear down the network:

```bash
task clean
```

## Example Projects

Use these example projects as starting points for common Solo workflows.

- [Address Book Example](https://github.com/hiero-ledger/solo/tree/main/examples/address-book)
- [Custom Network Config Example](https://github.com/hiero-ledger/solo/tree/main/examples/custom-network-config)
- [Local Build with Custom Config Example](https://github.com/hiero-ledger/solo/tree/main/examples/local-build-with-custom-config)
- [Multi-Cluster Backup and Restore Example](https://github.com/hiero-ledger/solo/tree/main/examples/multicluster-backup-restore)
- [Network with an External PostgreSQL Database Example](https://github.com/hiero-ledger/solo/tree/main/examples/external-database-test)
- [Network with Block Node Example](https://github.com/hiero-ledger/solo/tree/main/examples/network-with-block-node)
- [Network with Domain Names Example](https://github.com/hiero-ledger/solo/tree/main/examples/network-with-domain-names)
- [Node Create Transaction Example](https://github.com/hiero-ledger/solo/tree/main/examples/node-create-transaction)
- [Node Delete Transaction Example](https://github.com/hiero-ledger/solo/tree/main/examples/node-delete-transaction)
- [Node Update Transaction Example](https://github.com/hiero-ledger/solo/tree/main/examples/node-update-transaction)
- [One-Shot Falcon Deployment Example](https://github.com/hiero-ledger/solo/tree/main/examples/one-shot-falcon)
- [Rapid-Fire Example](https://github.com/hiero-ledger/solo/tree/main/examples/rapid-fire)
- [Solo Deployment with Hardhat Example](https://github.com/hiero-ledger/solo/tree/main/examples/hardhat-with-solo)
- [State Save and Restore Example](https://github.com/hiero-ledger/solo/tree/main/examples/state-save-and-restore)
- [Version Upgrade Test Example](https://github.com/hiero-ledger/solo/tree/main/examples/version-upgrade-test)
