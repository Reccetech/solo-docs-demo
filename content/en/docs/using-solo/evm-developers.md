---
title: "Using Solo for EVM Development"
weight: 105
description: >
  Learn how to use Solo's JSON-RPC relay for EVM workflows and integrate tools such as Hardhat for local smart contract development.
type: docs
---

## Using Solo for EVM Development

Solo can provision a local Hiero environment that includes a JSON-RPC relay, which allows EVM tooling (Hardhat, ethers, wallets, scripts) to work against your local network.

This guide is modeled on the Hardhat tutorial from Hedera docs and adapted for Solo-based workflows.

## Prerequisites

- Docker running locally with sufficient resources
- Solo installed and working
- Node.js installed
- Basic familiarity with Hardhat and ethers

## Step 1: Start a Solo Network with JSON-RPC Relay

Deploy a local Solo network with relay enabled:

```bash
solo one-shot single deploy
```

If you need explicit relay management in a manual deployment flow:

```bash
solo relay node add -i node1 --deployment "${SOLO_DEPLOYMENT}"
```

By default, the relay endpoint is available at:

- `http://localhost:7546`

## Step 2: Create and Initialize a Hardhat Project

```bash
mkdir solo-hardhat
cd solo-hardhat
npx hardhat --init
```

Choose a TypeScript or JavaScript starter project based on your preference.

## Step 3: Configure Hardhat for Solo Relay

Create/update `hardhat.config.ts` with a network that points to Solo's JSON-RPC relay:

```typescript
import type { HardhatUserConfig } from "hardhat/config";
import "@nomicfoundation/hardhat-toolbox";

const config: HardhatUserConfig = {
  solidity: "0.8.28",
  networks: {
    solo: {
      url: "http://127.0.0.1:7546",
      // Use a funded ECDSA private key from your local environment.
      // Keep real keys out of source control.
      accounts: [process.env.SOLO_EVM_PRIVATE_KEY ?? ""],
    },
  },
};

export default config;
```

Set your private key before running scripts:

```bash
export SOLO_EVM_PRIVATE_KEY=0xYOUR_PRIVATE_KEY
```

## Step 4: Build, Test, and Run

Build contracts:

```bash
npx hardhat build
```

Run tests:

```bash
npx hardhat test
```

Run a script on Solo:

```bash
npx hardhat run scripts/deploy.ts --network solo
```

## Step 5: Verify Transactions

Use one or more of the following:

- Explorer UI: `http://localhost:8080`
- Mirror REST API: `http://localhost:5551/api/v1/transactions?limit=1`
- JSON-RPC methods through `http://localhost:7546`

## Example: Simple ethers Transaction Script

```typescript
import { ethers } from "hardhat";

async function main() {
  const [sender] = await ethers.getSigners();
  console.log("Sender:", sender.address);

  const tx = await sender.sendTransaction({
    to: sender.address,
    value: 10_000_000_000n,
  });

  await tx.wait();
  console.log("Transaction confirmed");
}

main().catch((err) => {
  console.error(err);
  process.exit(1);
});
```

## Common Troubleshooting

- **Relay not reachable**: confirm Solo deployment completed and relay is running.
- **Account/key issues**: ensure you are using a valid funded ECDSA key for EVM tooling.
- **Port conflicts**: verify `7546` is free or update your network URL to match the forwarded port.

## Reference

For the full Hardhat walkthrough that inspired this page:

<https://docs.hedera.com/hedera/tutorials/smart-contracts/configuring-hardhat-with-hiero-local-node-a-step-by-step-guide>
