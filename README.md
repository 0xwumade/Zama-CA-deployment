Zama-CA-deployment 

🚀 Zama Creator Program — My First Contract Deployment (FHEVM + Hardhat)

As part of the #ZamaCreatorProgram, I deployed my first smart contract to Sepolia using Hardhat. Here's a quick summary 🧵


---

🛠 Step 1: Initialize Hardhat project

mkdir my-new-project && cd my-new-project
npx hardhat

> Choose "Create a basic sample project" and install dependencies.




---

🔐 Step 2: Install dotenv

npm install dotenv

Create a .env file:

INFURA_API_KEY=your_infura_key
PRIVATE_KEY=your_wallet_private_key


---

⚙ Step 3: Configure Hardhat for Sepolia

Edit hardhat.config.js:

require("dotenv").config();
require("@nomicfoundation/hardhat-toolbox");

module.exports = {
  solidity: "0.8.19",
  networks: {
    sepolia: {
      url: `https://sepolia.infura.io/v3/${process.env.INFURA_API_KEY}`,
      accounts: [process.env.PRIVATE_KEY],
    },
  },
};


---

📄 Step 4: Use the default Lock contract

Found in contracts/Lock.sol:

// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.9;

contract Lock {
    uint public unlockTime;
    address public owner;

    constructor(uint _unlockTime) payable {
        unlockTime = _unlockTime;
        owner = msg.sender;
    }

    function withdraw() public {
        require(block.timestamp >= unlockTime, "You can't withdraw yet");
        require(msg.sender == owner, "You aren't the owner");
        payable(msg.sender).transfer(address(this).balance);
    }
}


---

🧠 Step 5: Create a deploy script

Create scripts/deploy.js:

const hre = require("hardhat");

async function main() {
  const unlockTime = Math.floor(Date.now() / 1000) + 60;
  const lockedAmount = hre.ethers.parseEther("0.0001");

  const Lock = await hre.ethers.getContractFactory("Lock");
  const lock = await Lock.deploy(unlockTime, { value: lockedAmount });

  console.log("✅ Contract deployed to:", lock.target);
}

main().catch((error) => {
  console.error("🚨 Deployment failed:", error);
  process.exitCode = 1;
});


---

🚀 Step 6: Deploy to Sepolia

Make sure you have Sepolia test ETH in your wallet. Then run:

npx hardhat run scripts/deploy.js --network sepolia

Example output:

✅ Contract deployed to: 0xABC123456789...


---

✅ Done!

Smart contract deployed successfully on Sepolia using Hardhat & Zama-compatible tools.
