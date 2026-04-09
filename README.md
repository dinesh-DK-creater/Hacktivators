# GigPay (Hacktivators)

GigPay is a comprehensive Web3 FinTech platform designed for gig workers and international clients. It facilitates seamless fiat-to-crypto bridging, non-custodial on-chain wallet generation, and secure cross-border escrow payments natively through the browser.

## Architecture

The project is structured into three main modules:

### 1. Frontend (`/ Hacktivators Frontend`)
A modern web application built using **Next.js 16 (App Router)** and **React 19**.
- **Tech Stack**: Next.js, Radix UI, TailwindCSS, TypeScript.
- **Features**: User authentication logic, wallet dashboard, cross-border remittance gateway, and real-time transaction monitoring. 
- Integrated directly with the backend APIs mimicking on-chain and fiat bridges.

### 2. Backend (`/backend`)
A robust RESTful API built on **Node.js** & **Express**.
- **Tech Stack**: Node.js, Express, Tatum SDK, Razorpay, Ethers.js
- **Features**: 
  - Wallet API: Seamless creation of user wallets via Tatum SDK.
  - Payment Gateway: Razorpay integration to bridge Fiat (INR) entries/exits.
  - Escrow Logic: Serves as the intermediary that coordinates the smart contract locks for cross-border transactions implicitly mapping Fiat to MATIC.

### 3. Smart Contracts (`/smart contract`)
The immutable on-chain rules executing the payment locks via the **Hardhat** development environment.
- **Tech Stack**: Solidity, Hardhat, Ethers.
- **Features**: Contains the Escrow smart contracts that hold funds securely until gig work conditions are met or payment endpoints confirm completion.

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v18 or higher)
- npm or pnpm (for frontend)
- [Razorpay](https://razorpay.com/) Test Keys
- [Tatum](https://tatum.io/) API Key 

### Running the Backend Server
```bash
# Navigate to the backend directory
cd backend

# Install dependencies
npm install

# Setup environment variables
# Create a .env file and add your Tatum REST key and Razorpay configs
# PORT=5000
# TATUM_API_KEY=your_key...

# Start the server
npm run start
```
The backend will run on `http://localhost:5000`.

### Running the Frontend Application
```bash
# Navigate to the frontend directory
cd " Hacktivators Frontend"

# Install dependencies
npm install

# Start the Next.js development server
# If using Next.js 15+ and encounter BMI2 cpu issues, use build/start flow:
npm run build && npm run start

# Alternatively for standard dev mode:
npm run dev
```
The frontend is accessible at `http://localhost:3000`.

### Smart Contract Deployment
```bash
cd "smart contract"
npm install

# Compile contracts
npx hardhat compile

# Run tests
npx hardhat test

# Deploy to local node or testnet
npx hardhat run scripts/deploy.js --network mumbai
```

## How It Works (The Integration Flow)
1. User logs in/signs up on the frontend (`localhost:3000`).
2. An API call hits `/api/wallet/create` which creates a dedicated user wallet dynamically using Tatum.
3. The user initiates a **Send Money** transaction (converted from INR to MATIC).
4. The backend hits the `/api/escrow/lock` method to execute cross-border crypto locking, safely verified via smart contracts.

## License
MIT License
