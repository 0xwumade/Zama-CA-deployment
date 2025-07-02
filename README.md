Zama-CA-deployment 

🚀 Zama Creator Program — My First Contract Deployment (FHEVM + Hardhat)

As part of the #ZamaCreatorProgram, I deployed my first smart contract to Sepolia using Hardhat. Here's a quick summary 🧵

🛠 Step 1: Initialize Hardhat project
### 🚀 Deploy to Sepolia

```
npx hardhat run scripts/deploy.js --network sepolia
```
> Choose "Create a basic sample project"
Follow the prompts and install dependencies

🔐 Step 2: Install dotenv
'''
npm install dotenv
'''
Create a .env file in your root folder:

INFURA_API_KEY=your_infura_key
PRIVATE_KEY=your_wallet_private_key
