# ⚡HELPSWAP
A fully on-chain decentralized exchange built from scratch that enables **ETH ↔ TOKEN** swaps using an Automated Market Maker (AMM) model, modelled after Uniswap v1.

---

## 📖 Overview

This DEX implements the constant product formula `x * y = k` to facilitate permissionless token swaps. Liquidity providers deposit ETH and TOKEN into the pool and receive **LP tokens** representing their share. A **1% fee** is charged on every swap and distributed to liquidity providers.

---

##  Features

- 🔄 **ETH ↔ TOKEN Swaps** — Swap in either direction with slippage protection
- 💧 **Add & Remove Liquidity** — Deposit tokens to earn LP tokens; burn them to withdraw
- 🪙 **LP Tokens** — ERC-20 tokens minted proportionally to represent your pool share
- 💸 **1% Swap Fee** — Automatically applied on every swap, accruing to LPs
- 📐 **AMM Pricing** — Prices determined algorithmically via `x * y = (x + dx)(y - dy)`

---

## 🏗️ Architecture

### `Token.sol`
A simple ERC-20 token (`TKN`) with 1 million tokens minted to the deployer. Used as the trading pair on the exchange.

### `Exchange.sol`
The core DEX contract — itself an ERC-20 (for LP tokens). Handles:
- `addLiquidity` — Deposit ETH + TOKEN, receive LP tokens
- `removeLiquidity` — Burn LP tokens, receive back ETH + TOKEN
- `getOutputAmountFromSwap` — Pure AMM pricing calculation
- `ethToTokenSwap` — Swap ETH for TOKEN
- `tokenToEthSwap` — Swap TOKEN for ETH

---

## 📁 Project Structure

```
helpswap/
├── src/
│   ├── Token.sol
│   └── Exchange.sol
├── script/
│   └── Deploy.s.sol
├── test/
├── out/        # Compiled
└── README.md

---

## 🚀 Getting Started

### Prerequisites

- [Foundry](https://book.getfoundry.sh/getting-started/installation) installed

- A wallet funded with Sepolia ETH

### 1. Clone and set up

```bash
git clone https://github.com/shola-devv/HelpSwap.git
cd dex-app/foundry-app
forge install OpenZeppelin/openzeppelin-contracts
forge remappings > remappings.txt
```

### 2. Configure environment variables

Create a `.env` file inside `foundry-app/` with the following:

```env
PRIVATE_KEY="your_wallet_private_key"
RPC_URL="your_quicknode_sepolia_http_url"
ETHERSCAN_API_KEY="your_etherscan_api_key"
```

- **`PRIVATE_KEY`** — Export from MetaMask. Use a testnet-only wallet with no mainnet funds.
- **`RPC_URL`** — Create a free Sepolia endpoint at [QuickNode](https://www.quicknode.com), then copy the HTTP Provider URL.
- **`ETHERSCAN_API_KEY`** — Create a free account at [etherscan.io](https://etherscan.io) and generate an API key.

> ⚠️ Never commit your `.env` file. Make sure it's listed in `.gitignore`.

### 3. Compile contracts

```bash
forge build
```

### 4. Deploy contracts

```bash
source .env
forge script script/Deploy.s.sol --rpc-url $RPC_URL --private-key $PRIVATE_KEY --broadcast --verify --etherscan-api-key $ETHERSCAN_API_KEY
```

Note the deployed addresses for `Token` and `Exchange`.




ABIs are found inside `helpswap/out/<ContractName>.sol/<ContractName>.json` under the `"abi"` key after running `forge build`.

---

##  Live Deployment (Sepolia Testnet)

The contracts are deployed and verified on the Ethereum Sepolia testnet:

| Contract | Address |
|---|---|
| Token (TKN) | [`0x551c14f95Ce95792C6A65633E9F7853535617590`](https://sepolia.etherscan.io/address/0x551c14f95Ce95792C6A65633E9F7853535617590) |
| Exchange | [`0x0090497cCa1eA3bF77ccdc62A0b6c15F71c8EBc1`](https://sepolia.etherscan.io/address/0x0090497cCa1eA3bF77ccdc62A0b6c15F71c8EBc1) |

---

## 🧪 Testing the DEX

1. **Add liquidity** — Deposit ETH and TKN to receive LP tokens
2. **Swap ETH → TOKEN** — Enter an ETH amount, set slippage tolerance, swap
3. **Swap TOKEN → ETH** — Approve the exchange to spend your TKN, then swap
4. **Remove liquidity** — Burn your LP tokens to withdraw your share of the pool
5. **Verify on Etherscan** — Every transaction is fully on-chain

---

##  Tech Stack

| Layer | Technology |
|---|---|
| Smart Contracts | Solidity, Foundry |
| Token Standard | ERC-20 (OpenZeppelin) |
| AMM Model | Constant Product (`x * y = k`) |
| Frontend | Next.js, ethers.js |
| Network | Ethereum Sepolia Testnet |

---

## 📜 License

MIT

## Medium Article

ive written a medium article on the build process, find it here :  

## 👨 Author
 
shola Emmanuel Fayinminu  
Feel free to reach out or open an issue if you have questions.

Visit [http://sholaemmanuel.dev](http://sholaemmanuel.dev)
