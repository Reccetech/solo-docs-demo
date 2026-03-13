# Solo Documentation — Product Requirements Document

**Version:** 0.2  
**Date:** March 13, 2026  
**Status:** Draft

---

## Objective

Establish a simple, maintainable, and developer-focused documentation site for Solo that enables users to quickly:

1. Set up Solo *(primary goal)*
2. Debug Solo environments
3. Understand usage patterns (SDK and EVM)

The immediate priority (P0) is to deliver a minimal Hugo / Docsy documentation site focused on Solo setup and operational usability, with future expansion into automation and advanced workflows.

---

## Background

The current Solo documentation is embedded within the main Solo repository at [hiero-ledger/solo](https://github.com/hiero-ledger/solo). This has resulted in:

- Tight coupling between product code and documentation
- Higher maintenance overhead
- Fragmented developer journey
- Duplication in advanced setup materials
- Over-reliance on auto-generated documentation

To address this, documentation will be decoupled into a dedicated repository:

**[hiero-ledger/solo-docs](https://github.com/hiero-ledger/solo-docs)**

This enables:
- Independent documentation lifecycle
- Faster iteration via smaller PRs
- Clear ownership boundaries
- Simplified build and deployment pipeline
- Alignment with modern OSS documentation practices

Industry-leading developer documentation sites (including Hedera) provide a single canonical documentation experience, avoiding full-site versioning in favor of stable guides supported by release notes and migration documentation.

---

## Audience

| Persona | Description |
|---|---|
| **New user** | Developer evaluating Solo for the first time; needs a working network fast |
| **Application developer** | Building apps against a local Hiero network using SDKs or EVM tooling |
| **Platform / DevOps engineer** | Configuring custom topologies, CI pipelines, resource profiles |
| **Contributor** | Developer contributing to the Solo codebase itself |

---

## Build & Publishing Strategy

### Published URL

```
https://solo.hiero.org/
```

The site will **not** use versioned documentation paths (e.g., `https://solo.hiero.org/v<SOLO_VERSION>/`).

### Rationale for No Full-Site Versioning

- Solo setup and debugging guidance should remain consistent across releases
- Versioned full-site documentation increases maintenance overhead
- Users should not need to select a version before learning how to use Solo

### Handling Version-Specific Changes

Release-specific differences will be handled through:
- Release notes
- Migration / upgrade guides
- CLI reference updates
- Targeted compatibility notes

### Publishing Requirements

- Documentation built from `hiero-ledger/solo-docs`
- GitHub Actions builds and deploys to `solo.hiero.org`
- Deterministic local builds must be supported
- The site should always reflect the current recommended Solo workflow

---

## Execution Strategy

### Documentation Generation

- **CLI documentation** remains auto-generated — targeted as a **P2** initiative
- All other auto-generated documentation has been removed to reduce complexity
- All remaining documentation is manually maintained until Solo stabilizes

### Versioning

- Solo documentation will not support full-site versioning
- Guides must remain valid across releases wherever possible
- Version-specific differences are handled outside core setup guides

---

## Left-Hand Navigation Structure

The left navigation is scoped to the **Docs** section of the site. Items are listed in display order.

---

### 1. Simple Solo Setup

**Goal:** Get any new user to a running local Hiero network in one session with as little friction as possible.

Contents should cover:
- System prerequisites (RAM, CPU, supported platforms)
- Installation instructions for macOS, Linux, and Windows (WSL2) via Homebrew and other package managers
- One-command deployment (`solo one-shot single deploy`) as the primary happy path
- Basic lifecycle operations: stop, start, restart, and upgrade
- Teardown and cleanup procedures

*This is the entry point for the majority of users. It must be self-contained and require no prior Solo knowledge.*

---

### 2. Advanced Solo Setup

**Goal:** Give platform engineers and CI users precise control over network topology, configuration, diagnostics, and upgrades.

This section is a parent container. Its children are listed below.

---

#### 2.1 Advanced Network Deployments

**Goal:** Document step-by-step manual deployment workflows and Helm-level customization for users who need full control over how a network is brought up.

Contents should cover:
- Falcon deployment pattern
- Manual step-by-step network initialization sequence
- Customizing Helm chart values
- Dynamic node addition and deletion

---

#### 2.2 Solo CLI

**Goal:** Serve as the canonical command reference for the Solo CLI so users can look up any command, flag, or output option without reading narrative guides.

Contents should cover:
- Full command and subcommand listing
- `--output` flag options and formats
- Legacy-to-current command migration table
- All global and per-command flags with descriptions

*Note: CLI docs are targeted for auto-generation as a P2 initiative. Until then, this page is manually maintained.*

---

#### 2.3 Hiero Consensus Node Platform Developer

**Goal:** Guide platform engineers who need to build, configure, or extend Hiero consensus nodes at the platform layer within a Solo-managed network.

Contents should cover:
- Platform-level setup and configuration for consensus nodes
- Integration points between Solo and the Hiero platform layer
- Relevant configuration flags and environment considerations

---

#### 2.4 Hiero Consensus Node Execution Developer

**Goal:** Support developers working at the execution layer of the consensus node — those who need to run, debug, or modify node execution behavior within Solo.

Contents should cover:
- Execution-layer setup within a Solo network
- How to configure nodes for custom execution scenarios
- Interaction patterns between the execution layer and Solo lifecycle commands

---

#### 2.5 Attach JVM Debugger and Retrieve Logs

**Goal:** Enable developers to inspect the internals of a running consensus node for debugging, profiling, or log retrieval.

Contents should cover:
- Using `k9s` to access container logs
- Attaching a remote JVM debugger from IntelliJ IDEA
- Saving and reusing network state snapshots

---

#### 2.6 Using Environment Variables

**Goal:** Provide a complete reference of all environment variables that influence Solo's behavior, so users can tune deployments without modifying config files.

Contents should cover:
- Full table of supported environment variables
- Default values for each variable
- Categories: paths, logging, chain ID, ports, operator keys

---

#### 2.7 Solo CI Workflow

**Goal:** Show platform and DevOps engineers how to integrate Solo network deployment into automated CI pipelines.

Contents should cover:
- GitHub Actions runner requirements
- Docker resource checks needed before deployment
- Example workflow YAML demonstrating a full deploy-test-destroy cycle

---

#### 2.8 API Reference

**Goal:** Direct developers to the versioned TypeDoc API reference so they can programmatically integrate with or extend Solo.

Contents should cover:
- URL pattern for the versioned API reference (`solo.hiero.org/v<VERSION>/classes/`)
- Brief description of what is covered (methods, classes, properties)
- Link to the live reference

---

#### 2.9 Using "Task" and Examples

**Goal:** Help users get a network running quickly from a cloned Solo repository using the `task` Taskfile runner, and point them to community example projects.

Contents should cover:
- Installing and using the `task` tool
- Available Taskfile targets for bringing up a local network
- Links to maintained GitHub example repositories

---

### 3. Using Solo

**Goal:** Help application developers build against a running Solo network using their preferred SDK or toolchain.

This section is a parent container. Its children are listed below.

---

#### 3.1 Using Solo with Hiero SDKs

**Goal:** Walk a JavaScript/TypeScript developer through submitting their first transaction to a local Solo network.

Contents should cover:
- Launching the network as a prerequisite
- Installing the Hiero JavaScript SDK
- Creating test accounts
- Submitting transactions and reading receipts
- Running example scripts end-to-end

---

#### 3.2 Using Solo for EVM Development

**Goal:** Enable EVM developers to point their existing Ethereum tooling (Hardhat, ethers.js, MetaMask) at a local Hiero network via the JSON-RPC relay.

Contents should cover:
- Enabling and configuring the JSON-RPC relay on a Solo network
- Connecting Hardhat to the relay endpoint
- Deploying and interacting with a Solidity contract
- Wallet and network configuration

---

#### 3.3 Using Network Load Generator with Solo

**Goal:** Give performance engineers and benchmark users a way to stress-test a Solo network and measure throughput.

Contents should cover:
- Deploying the Network Load Generator (NLG) against a running Solo network
- Configuring test parameters (TPS targets, transaction types)
- Reading and interpreting results

---

#### 3.4 Accessing Solo Services

**Goal:** Help developers locate and connect to the ancillary services that Solo can deploy alongside the consensus network.

Contents should cover:
- Accessing the **Mirror Node Explorer** (block explorer UI)
- Connecting to **Block Nodes** for chain data
- Using **Relay services** (JSON-RPC relay endpoint configuration and connection)
- Port mappings and service discovery within the cluster

---

### 4. FAQ

**Goal:** Answer the most common questions users ask before and after their first deployment, reducing friction and support load.

Contents should cover:
- One-command deployment options and variants
- How to fully destroy a network and clean up resources
- How to access exposed services (mirror node, relay, explorer)
- Common usage patterns and gotchas

---

### 5. Troubleshooting

**Goal:** Help users self-diagnose and fix the most common failure modes without filing a support request.

Contents should cover:
- Pods not reaching Ready state
- CrashLoopBackOff causes and remediation
- Resource constraint errors (CPU/RAM/disk)
- Stale artifacts from a prior installation interfering with a fresh deploy
- Where to get help (Discord, GitHub Issues)

---

### 6. Contributing

**Goal:** Orient first-time contributors to the Solo project and set expectations around the contribution process.

Contents should cover:
- How to set up a local development environment
- Running the test suite
- Contribution guidelines and code standards
- Link to the Hiero `.github` CONTRIBUTING.md

---

## Top-Level Navigation Sections

These sections appear in the site header and have their own left-nav trees separate from Docs.

### Development

**Goal:** Guide contributors who are building or modifying Solo itself (as distinct from users running it).

| Page | Goal |
|---|---|
| **Contributing to Hiero Projects** | Redirect to the canonical Hiero contribution guidelines on GitHub |
| **Solo API Reference** | Link to the full TypeDoc reference for the Solo source code (methods, classes, interfaces) |

---

## Success Criteria

This initiative succeeds when:

- [ ] New developers can deploy Solo without external assistance
- [ ] Documentation reflects real developer workflow phases
- [ ] Advanced setup duplication is eliminated
- [ ] Documentation can be built and deployed reproducibly
- [ ] Docs iteration velocity increases through smaller PR workflow

---

## Scope Boundaries

### In Scope — P0

- Creation of dedicated Solo docs repository at `hiero-ledger/solo-docs`
- Documentation restructuring per the navigation structure defined in this PRD
- Setup and debugging documentation improvements
- CI/CD deployment pipeline to `solo.hiero.org`

### In Scope — P1

- CLI docs auto-generation
- Videos, blogs, and other supplementary content on Solo setup and usage

### Out of Scope (Initial Phase)

- Full automation frameworks
- Multi-version documentation UX

---

## Not Published (Current)

The following content exists in the repository but is not surfaced as user-facing docs at this time:

| Content | Notes |
|---|---|
| `migration/legacy-versions.md` | Version compatibility matrix; candidate for a future release notes or compatibility page |
| `migration/contributing/onboarding_questions.md` | Internal onboarding Q&A; not intended for public docs |
| `migration/workshops/devcon_2024_fall_workshop.md` | DevCon 2024 workshop guide; candidate for P1 "Videos & Blogs" content or a Tutorials section |
| `migration/design/archive/` | Draft design documents; internal reference only |
| `migration/design/architecture/` | Architecture design documents; candidate for a future Architecture section under Development |
