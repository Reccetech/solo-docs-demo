---
title: "Solo CLI"
weight: 40
aliases:
  - /docs/solo-cli/
  - /docs/solo-commands/
  - /docs/cli-migrations/
description: >
    Unified Solo CLI documentation, including the user manual, command mappings, and command reference.
type: docs
---

## Solo CLI User Manual

Solo has a series of commands to use, and some commands have subcommands.
User can get help information by running with the following methods:

`solo --help` will return the help information for the `solo` command to show which commands
are available.

### Version Information

Check the Solo version using:

```bash
solo --version
```

For machine-readable output formats (Kubernetes ecosystem standard), use the `--output` or `-o` flag:

```bash
solo --version -o json    # JSON format: {"version": "0.46.1"}
solo --version -o yaml    # YAML format: version: 0.46.1
solo --version -o wide    # Plain text: 0.46.1
```

The `--output` flag can also be used with other Solo commands to suppress banners and produce machine-readable output, making it ideal for scripts and CI/CD pipelines.

`solo command --help` will return the help information for the specific command to show which options

```text
solo ledger account --help

Manage Hedera accounts in solo network

Commands:
  system init     Initialize system accounts with new keys
  account create   Creates a new account with a new key and stores the key in th
                   e Kubernetes secrets, if you supply no key one will be genera
                   ted for you, otherwise you may supply either a ECDSA or ED255
                   19 private key
  account update   Updates an existing account with the provided info, if you wa
                   nt to update the private key, you can supply either ECDSA or
                   ED25519 but not both

  account get      Gets the account info including the current amount of HBAR

Options:
      --dev                 Enable developer mode                      [boolean]
      --force-port-forward  Force port forward to access the network services
                                                                       [boolean]
  -h, --help                Show help                                  [boolean]
  -v, --version             Show version number                        [boolean]
```

`solo command subcommand --help` will return the help information for the specific subcommand to show which options

```text
solo ledger account create --help

Creates a new account with a new key and stores the key in the Kubernetes secret
s, if you supply no key one will be generated for you, otherwise you may supply
either a ECDSA or ED25519 private key

Options:
      --dev                  Enable developer mode                     [boolean]
      --force-port-forward   Force port forward to access the network services
                                                                       [boolean]
      --hbar-amount          Amount of HBAR to add                      [number]
      --create-amount        Amount of new account to create            [number]
      --ecdsa-private-key    ECDSA private key for the Hedera account   [string]
  -d, --deployment           The name the user will reference locally to link to
                              a deployment                              [string]
      --ed25519-private-key  ED25519 private key for the Hedera account [string]
      --generate-ecdsa-key   Generate ECDSA private key for the Hedera account
                                                                       [boolean]
      --set-alias            Sets the alias for the Hedera account when it is cr
                             eated, requires --ecdsa-private-key       [boolean]
  -c, --cluster-ref          The cluster reference that will be used for referen
                             cing the Kubernetes cluster and stored in the local
                              and remote configuration for the deployment.  For
                             commands that take multiple clusters they can be se
                             parated by commas.                         [string]
  -h, --help                 Show help                                 [boolean]
  -v, --version              Show version number                       [boolean]
```

## Updated CLI Command Mappings

The following tables provide a mapping of previous (`< v0.44.0`) CLI commands to their updated structure.

### Init

| Old Command | New Command |
|---|---|
| `init` | No changes |

### Block node

| Old Command | New Command |
|---|---|
| `block node add` | No changes |
| `block node destroy` | No changes |
| `block node upgrade` | No changes |

### Account

| Old Command | New Command |
|---|---|
| `account init` | `ledger system init` |
| `account update` | `ledger account update` |
| `account create` | `ledger account create` |
| `account get` | `ledger account info` |

### One Shot

| Old Command | New Command |
|---|---|
| `quick-start single deploy` | `one-shot single deploy` |
| `quick-start single destroy` | `one-shot single destroy` |

### Cluster Reference

| Old Command | New Command |
|---|---|
| `cluster-ref connect` | `cluster-ref config connect` |
| `cluster-ref disconnect` | `cluster-ref config disconnect` |
| `cluster-ref list` | `cluster-ref config list` |
| `cluster-ref info` | `cluster-ref config info` |
| `cluster-ref setup` | `cluster-ref config setup` |
| `cluster-ref reset` | `cluster-ref config reset` |

### Deployment

| Old Command | New Command |
|---|---|
| `deployment add-cluster` | `deployment cluster attach` |
| `deployment list` | `deployment config list` |
| `deployment create` | `deployment config create` |
| `deployment delete` | `deployment config delete` |

### Explorer

| Old Command | New Command |
|---|---|
| `explorer deploy` | `explorer node add` |
| `explorer destroy` | `explorer node destroy` |

### Mirror Node

| Old Command | New Command |
|---|---|
| `mirror-node deploy` | `mirror node add` |
| `mirror-node destroy` | `mirror node destroy` |

### Relay

| Old Command | New Command |
|---|---|
| `relay deploy` | `relay node add` |
| `relay destroy` | `relay node destroy` |

### Network

| Old Command | New Command |
|---|---|
| `network deploy` | `consensus network deploy` |
| `network destroy` | `consensus network destroy` |

### Node

| Old Command | New Command |
|---|---|
| `node keys` | `keys consensus generate` |
| `node freeze` | `consensus network freeze` |
| `node upgrade` | `consensus network upgrade` |
| `node setup` | `consensus node setup` |
| `node start` | `consensus node start` |
| `node stop` | `consensus node stop` |
| `node restart` | `consensus node restart` |
| `node refresh` | `consensus node refresh` |
| `node add` | `consensus node add` |
| `node update` | `consensus node update` |
| `node delete` | `consensus node destroy` |
| `node add-prepare` | `consensus dev-node-add prepare` |
| `node add-submit-transaction` | `consensus dev-node-add submit-transactions` |
| `node add-execute` | `consensus dev-node-add execute` |
| `node update-prepare` | `consensus dev-node-update prepare` |
| `node update-submit-transaction` | `consensus dev-node-update submit-transactions` |
| `node update-execute` | `consensus dev-node-update execute` |
| `node upgrade-prepare` | `consensus dev-node-upgrade prepare` |
| `node upgrade-submit-transaction` | `consensus dev-node-upgrade submit-transactions` |
| `node upgrade-execute` | `consensus dev-node-upgrade execute` |
| `node delete-prepare` | `consensus dev-node-delete prepare` |
| `node delete-submit-transaction` | `consensus dev-node-delete submit-transactions` |
| `node delete-execute` | `consensus dev-node-delete execute` |
| `node prepare-upgrade` | `consensus dev-freeze prepare-upgrade` |
| `node freeze-upgrade` | `consensus dev-freeze freeze-upgrade` |
| `node logs` | `deployment diagnostics logs` |
| `node states` | `consensus state download` |

## Solo Command Reference

This section consolidates command-reference content from the v0.57.0 `Solo CLI Commands` page.

### Table of Contents

- Root Help Output
- init
- config
  - config ops
    - config ops backup
    - config ops restore-config
    - config ops restore-clusters
    - config ops restore-network
- block
  - block node
- cluster-ref
  - cluster-ref config
- consensus
  - consensus network
  - consensus node
  - consensus state
  - consensus dev-node-add / update / upgrade / delete / freeze
- deployment
  - deployment cluster / config / diagnostics
- explorer
- keys
- ledger
- mirror
- relay
- one-shot
- rapid-fire

### Root Help Output

```text
Usage:
  solo <command> [options]

Commands:
  init
  config
  block
  cluster-ref
  consensus
  deployment
  explorer
  keys
  ledger
  mirror
  relay
  one-shot
  rapid-fire
```

### config ops

```text
config ops

Configuration backup and restore operations

Commands:
  config ops backup
  config ops restore-config
  config ops restore-clusters
  config ops restore-network
```

#### config ops backup

```text
config ops backup

Display backup plan for all component configurations of a deployment.

Required:
  -d, --deployment

Common options:
  --output-dir
  --zip-file
  --zip-password
  -q, --quiet-mode
  -v, --version
```

### rapid-fire

```text
rapid-fire

Commands for performing load tests on a Solo deployment.

Commands:
  rapid-fire load start
  rapid-fire load stop
  rapid-fire destroy all
```

For the full v0.57.0 command-by-command option details, see:
https://solo.hiero.org/v0.57.0/docs/solo-commands/#config-ops-backup
