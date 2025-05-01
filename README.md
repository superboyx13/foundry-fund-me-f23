# 🚀 Foundry Fund Me (CU Fork)

A smart contract project using Foundry, designed for decentralized funding and testing on zkSync and Sepolia.

---

## 🛠 Getting Started

### 🔧 Requirements

- **Git**
  ```bash
  git --version
  # Expected: git version x.x.x
  ```

- **Foundry**
  ```bash
  forge --version
  # Expected: forge 0.2.0 (816e00b 2023-03-16T00:05:26.396218Z)
  ```

---

## ⚡ Quickstart

```bash
git clone https://github.com/superboyx13/foundry-fund-me-f23/tree/master
cd foundry-fund-me-f23
make
```

### 💻 Optional: Use Gitpod

Don't want to install locally? Use [Gitpod](https://gitpod.io/) to launch in a dev environment instantly.

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/Cyfrin/foundry-fund-me-cu)

---

## 📦 Usage

### 🔁 Deploy

```bash
forge script script/DeployFundMe.s.sol
```

---

## ✅ Testing

We cover 4 test tiers:

1. **Unit**
2. **Integration**
3. **Forked** ✅
4. **Staging** ✅

Run tests:
```bash
forge test
```

Run specific test:
```bash
forge test --match-test testFunctionName
```

Test coverage:
```bash
forge coverage
```

---

## 🌐 Local zkSync Setup

### 🧩 Additional Requirements

- **foundry-zksync**
  ```bash
  forge --version
  # Expected: forge 0.0.2 (zkSync)
  ```

- **Node + npm + npx**
  ```bash
  npm --version   # e.g., 7.24.0
  npx --version   # e.g., 8.1.0
  ```

- **Docker**
  ```bash
  docker --version   # e.g., Docker version 20.10.7
  docker --info      # Should show `Context: default`
  ```

---

### 🧪 Start zkSync Local Node

```bash
npx zksync-cli dev config
# Choose: In memory node, no additional modules

npx zksync-cli dev start
```

Expected output:
```
In memory node started v0.1.0-alpha.22
Chain ID: 260
RPC URL: http://127.0.0.1:8011
```

Reference: [zkSync Rich Accounts](https://era.zksync.io/docs/tools/testing/era-test-node.html#use-pre-configured-rich-wallets)

---

### 🚀 Deploy to zkSync Local Node

```bash
make deploy-zk
```

---

## 🔐 Deployment to Sepolia Testnet

### 🧾 Environment Variables

Create a `.env` file (see `.env.example`) and define:

```dotenv
PRIVATE_KEY=your_private_key   # Don't use a key with real funds
SEPOLIA_RPC_URL=https://your-sepolia-node-url
ETHERSCAN_API_KEY=your_key     # Optional
```

Get testnet ETH: [Chainlink Faucets](https://faucets.chain.link)

### 🛰 Deploy to Sepolia

```bash
forge script script/DeployFundMe.s.sol \
  --rpc-url $SEPOLIA_RPC_URL \
  --private-key $PRIVATE_KEY \
  --broadcast \
  --verify \
  --etherscan-api-key $ETHERSCAN_API_KEY
```

---

## 📜 Scripts

Interact after deploying:

### Fund

```bash
cast send <FUNDME_CONTRACT_ADDRESS> "fund()" \
  --value 0.1ether \
  --private-key <PRIVATE_KEY>
```

OR

```bash
forge script script/Interactions.s.sol:FundFundMe \
  --rpc-url sepolia \
  --private-key $PRIVATE_KEY \
  --broadcast
```

### Withdraw

```bash
forge script script/Interactions.s.sol:WithdrawFundMe \
  --rpc-url sepolia \
  --private-key $PRIVATE_KEY \
  --broadcast
```

OR

```bash
cast send <FUNDME_CONTRACT_ADDRESS> "withdraw()" \
  --private-key <PRIVATE_KEY>
```

---

## ⛽ Estimate Gas

```bash
forge snapshot
```

Output: `.gas-snapshot` file with cost estimates.

---

## 🎨 Formatting

```bash
forge fmt
```

---
