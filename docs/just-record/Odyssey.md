---
sidebar_position: 2
---

# Odyssey

## Main Link

| Useful Link        |   Halving Date            |  
|:---------------------:|:-------------------:|
|  diamondswap  |  https://diamondswap.com/exchange     |
|  Bridge  |  https://portal.dioneprotocol.com     |
|  Test Dione Faucet  |  https://portal.dioneprotocol.com/faucet     |
|  Testnet Explorer | [https://testnet.odysseyscan.com](https://testnet.odysseyscan.com)       |
|  Mainnet Explorer | [https://odysseyscan.com/](https://odysseyscan.com/)       |
|  Dione verification | npx hardhat --network dione etherscan-verify --api-url https://api.odysseyscan.com//api/v1/ --api-key 123     |
|  Dione Test verification | npx hardhat --network dione_test etherscan-verify --api-url https://api-testnet.odysseyscan.com//api/v1/ --api-key 123     |
|  matic_test | npx hardhat --network matic_test etherscan-verify --api-url https://api-amoy.polygonscan.com --api-key IA769E8IXSJMNP9AGHC9QYX25TWS2E1JUP    |
|  Matic  | npx hardhat --network matic etherscan-verify --api-key IA769E8IXSJMNP9AGHC9QYX25TWS2E1JUP    |
|  Celo Test  | npx hardhat --network celo_test etherscan-verify --api-url https://api-alfajores.celoscan.io --api-key VGRXNYA5HSJQMRRYKCQHUIMCFGJV63N6UU   |
|  Celo  | npx hardhat --network celo etherscan-verify --api-url https://api.celoscan.io --api-key VGRXNYA5HSJQMRRYKCQHUIMCFGJV63N6UU   |

+ Deploy Wrapped token

  + https://docs.dioneprotocol.com/odyssey-guide-to-mainnet/onboarding-guide/getting-started/your-first-odyssey-dapp-token/deploying-on-odyssey-chain-as-an-existing-evm-project

  + Deploying smart contracts

    https://docs.dioneprotocol.com/smart-contract-and-token-deployment/deploying-smart-contracts
    

+ Token on Odyssey

  + Odyssey Mainnet

    | Token | Address  | Name  | symbol |
    |:---------------------:|:-------------------:|:---------------:|:------------:|
    | USDC | 0x8aBEE32587864cce7000e6f2820680874eD6100A |       |         |
    | Wrapped ART | 0x953AAc5A0205CCdD6E0b4107ffB0a0ef7155F5bE |   Wrapped Arkreen REC Token    |  wART       |
    | Wrapped AKRE | 0x960C67B8526E6328b30Ed2c2fAeA0355BEB62A83 |   Wrapped Arkreen Token    |  wAKRE       |

  + Odyssey Testnet

    | Token | Address  | Name  | symbol |
    |:---------------------:|:-------------------:|:---------------:|:------------:|
    | USDC                  |     |        |         |
    | Wrapped AKRE（X）     | 0xd83C9743B17426C28Cf3FD12966cc9873D009ABF   |   Wrapped Arkreen Token     |   wAKRE     |
    | Wrapped ART           | 0xd092e1f47d4e5d1C1A3958D7010005e8e9B48206   |   Wrapped Arkreen REC Token |   wART     |
    | Wrapped AKRE         | 0xeb0a8d25cc479825e6Ca942D516a1534C32dFBe4 |   Wrapped Arkreen Token    |  wAKRE       |

+ Mainnet RPC

| Name | Odyssey Chain Mainnet  |
|:---------------------:|:-------------------:|
| RPC URL  | https://node.dioneprotocol.com/ext/bc/D/rpc |
| ChainID | 153153 |
| Symbol  | DIONE |
| Decimals  | 18 |
| Explorer  |  https://odysseyscan.com |

+ Testnet RPC

| Name      |   Odyssey Chain Testnet  |
|:---------------------:|:-------------------:|
| RPC URL    |  https://testnode.dioneprotocol.com/ext/bc/D/rpc |
| ChainID    |  131313 |
| Symbol     |   DIONE |
| Decimals   | 18 |
| Explorer   |  https://testnet.odysseyscan.com |

+ Dione Spark Grant

Dione Spark Grant Recipients Only - Dione Protocol will fund the $DIONE side of the LP via reimbursement upon locking of the trading pair for 6 months minimum via Trustswap, in addition to co-marketing on all socials.

All grants will be approved on case to case basis after on internal review.



+ Flatten 

  + npx hardhat flatten contracts/Arkreen/WrappedToken.sol flatten/WrappedToken.sol


  + npx hardhat --network celo etherscan-verify --api-url https://api.celoscan.io --api-key VGRXNYA5HSJQMRRYKCQHUIMCFGJV63N6UU