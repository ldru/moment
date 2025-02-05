---
sidebar_position: 1
---

**# Solana Memo**

  + Integrate Raydium Swap Functionality on a Solana Program
    + https://blockchain.oodles.io/dev-blog/integrate-raydium-swap-functionality-solana-program/

  + Solana rpc:
    + https://mainnet.helius-rpc.com/?api-key=36703baf-8e23-46df-8330-bda161b61c5b
    + https://devnet.helius-rpc.com/?api-key=36703baf-8e23-46df-8330-bda161b61c5b
    + https://solana-mainnet.api.syndica.io/api-key/4fPYAGY635k6X9RJqEay7DLU4bVJAbTm25d7bNJ9gHf145Xc8u3Q7pPxzktzUWsEsmzdgZbSfdowBNqmGTY8Xfv8ZJ5PpqXT6fF
    + https://solana-mainnet.api.syndica.io/api-key/4eXtFnQmp1C1eRZoWcSutx6uBGVSJjKYkUoQ2JGYNmTt8cE7mzt4qcmjRrkxh3UkCTYQ28zfPAU61ZozKPcRQgXe5uiFXzCC1eS


```

const { expect } = require('chai');
const BN = require('bn.js');

// Custom deep comparison for BN instances
function deepEqualWithBN(obj1, obj2) {
  const keys1 = Object.keys(obj1);
  const keys2 = Object.keys(obj2);

  if (keys1.length !== keys2.length) return false;

  for (let key of keys1) {
    const val1 = obj1[key];
    const val2 = obj2[key];

    if (BN.isBN(val1) && BN.isBN(val2)) {
      if (!val1.eq(val2)) return false;
    } else if (typeof val1 === 'object' && typeof val2 === 'object') {
      if (!deepEqualWithBN(val1, val2)) return false;
    } else {
      if (val1 !== val2) return false;
    }
  }

  return true;
}

describe('Custom object comparison with BN.js', () => {
  it('should compare objects with BN instances using custom function', () => {
    const obj1 = {
      balance: new BN('1000000000000000000'),
      user: '0x1234',
      nested: { amount: new BN('500') }
    };

    const obj2 = {
      balance: new BN('1000000000000000000'),
      user: '0x1234',
      nested: { amount: new BN('500') }
    };

    expect(deepEqualWithBN(obj1, obj2)).to.be.true;
  });
});

```

**Create Pool**
  1. https://explorer.solana.com/tx/2EcNEQ26WSbojGfwEy5csvy1RDnnbVhCfXXHqED5YCTE4atwZbR8Kx659pPokHhy4CysnNqYmLsP5MSrdj5ia5yK

**ART Pool**
  https://app.meteora.ag/dlmm/create
  https://raydium.io/clmm/create-pool
  https://jup.ag/
  ART: art8zaVhaKBZp6sVeVd72oQoKseFqwNDcxGW32VBe1Q
  USDC: EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v

  https://raydium.io/swap/?inputMint=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v&outputMint=art8zaVhaKBZp6sVeVd72oQoKseFqwNDcxGW32VBe1Q

  交易对:   AXuNiMC5mtoVQMyEJqtZ9Y8t1pohfmfaF3CRav29s3Hn
  ART:      FPHsi4sMUWvVkimfzkQHoF9BiC1AWwGco3KVmGDsEcCs
  USDC:     6s77TzqDR4rBqqqRxYhodYKCkprS3ynH8iRTjKxYkc6r



**How the accounts for EVM-based blockchains (like Ethereum) and Solana are linked together**
  ```
    EVM (Ethereum):
    Derivation path: m/44'/60'/0'/0/n
    Here, 60 is the coin type for Ethereum, and n is the account index (e.g., 0 for the first account).
    Solana:
    Derivation path: m/44'/501'/0'/0/n
    Here, 501 is the coin type for Solana, and n is the account index.
  ```

**+ Solana 密钥格式**
  1. Solana 钱包的的密钥包括 32字节的私钥和32字节的公钥。有两种格式，一是 Uint8Array, 一是Uint8Array的Base58编码;
  2. 32字节的短密钥，可以通过 Keypair.fromSeed(secretKey)转为Solana 密钥对;
  3. 64字节的完全密钥，可以通过 Keypair.fromSecretKey(privateKey) 转为Solana 密钥对;
  4. Uint8Array 格式的密钥转为 base58编码: bs58.encode(secretKey);
  5. base58编码的密钥转为Uint8Array格式: bs58.decode(privateKeyBase58);
  6. Hex 格式的密钥转为Uint8Array格式: Buffer.from(privateKey, "hex");
  7. Uint8Array 格式的密钥转为Hex格式: Buffer.from(secretKey).toString("hex");

**+ How to run AREC Demo Dapp on Solana Dapp**
  + E:\BlockchainWallet\Argon\solana22\arec-sol-demo
  + ()
  + yarn dev

**+ How to recover the deployment**
  1. solana-keygen recover -o recover.json --force
  ```
    >> [recover] seed phrase:  (Copy and paste the 12-word seed phrase)
    >> [recover] If this seed phrase has an associated passphrase, enter it now. Otherwise, press ENTER to continue: (Input ENTER)
    >> Recovered pubkey `"7KMvcE5UUrDYadWuFakgDwUq6rYQmZBaBa5T7KbEnrxC"`. Continue? (y/n):   (Input y)
    >> Wrote recovered keypair to recover.json
  ```
  2. solana program deploy --buffer recover.json /home/ldru/solana/ArkreenSol/target/deploy/arec_sol.so

**+ Solana command list**
1. anchor build
1. anchor keys list
2. anchor keys sync
3. solana config get
4. solana balance
5. solana address
6. solana airdrop 5
7. solana program close --buffers --buffers [ACCOUNT_ADDRESS]
8. solana program close [PROGRAM_ID]
9. anchor test --skip-deploy
10. anchor test --skip-local-validator		(!!!!!!!!!!!!!!!!!!!!)
11. solana-test-validator --reset

**+ WormHole Bridge**

  **1. Importance**

    |   Item             |   Importance           |  
    |:---------------------:|:-------------------:|
    | Project folder        |  E:\BlockchainWallet\Argon\wormhole\wormhole-sdk-ts\examples     |
    |  创建包裹的Token      | $ tsx src/createWrapped.ts       |
    |  Bridge Token       | $ tsx src/tokenBridge.ts       |
    |  测试Log            | E:\BlockchainWallet\Argon\wormhole\wormhole-sdk-ts\examples\log.txt      |
    |  安装wormhole SDK   | npm install @wormhole-foundation/sdk      |
    |  部署包裹 ART       | cd E:\BlockchainWallet\Argon\SolanaBridge;  yarn wrapped    |
    |  portalbridge       | https://portalbridge.com/advanced-tools    |
    |  生成Lucky地址       | E:\BlockchainWallet\Argon\solana22\ArkreenSol\tests\utils\mint-arec-basics.ts    |


  **2. Links**

    | Useful Link        |   Useful Link URL            |  
    |:-------------------------:|:-------------------:|
    |  Chain IDs                |  https://wormhole.com/docs/build/reference/chain-ids/     |
    |  Contract Addresses       | https://wormhole.com/docs/build/reference/contract-addresses/       |
    |  Wormhole TypeScript SDK  | https://wormhole.com/docs/build/applications/wormhole-sdk/wormhole-sdk/       |
    |  Wormhole TS SDK Docs     | https://wormhole-foundation.github.io/wormhole-sdk-ts/       |

  **3. How to setup the envirormnet for programs**

```
        git clone  https://github.com/wormhole-foundation/wormhole-sdk-ts.git
        cd wormhole-sdk-ts
        npm install
        npm run build
        cd examples
        ```

        2) Optionally modify token bridge or cctp programs

        3) run stuff

        ```sh
        npm run tb
        # or
        npm run cctp
        # or
        npm run gateway
```

```
      Ploygon Mainnet: 
      contracts: {
        coreBridge: '0x7A4B5a56256163F07b2C80A7cA55aBE66c4ec4d7',
        tokenBridge: '0x5a58505a96D1dbf8dF91cB21B54419FC36e93fdE',
        nftBridge: '0x90BBd86a6Fe93D3bc3ed6335935447E75fAb7fCf',
        relayer: '0x27428DD2d3DD32A4D7f7C497eAaa23130d894911',
        tokenBridgeRelayer: '0xcafd2f0a35a4459fa40c0517e17e6fa2939441ca',
        cctp: {
          tokenMessenger: '0x9daF8c91AEFAE50b9c0E69629D3F6Ca40cA3B3FE',
          messageTransmitter: '0xF3be9355363857F3e001be68856A2f96b4C39Ba9',
          wormholeRelayer: '0x4cb69FaE7e7Af841e44E1A1c30Af640739378bb2',
          wormhole: '0x0FF28217dCc90372345954563486528aa865cDd6'
        },
        portico: {
          porticoUniswap: '0x227bABe533fa9a1085f5261210E0B7137E44437B',
          uniswapQuoterV2: '0x61fFE014bA17989E743c5F6cB21bF9697530B21e',
          porticoPancakeSwap: undefined,
          pancakeSwapQuoterV2: undefined
        }
      },

```

  **3. Bridge Steps**
    **STep 1**
      Celo: Function: attestToken(address tokenAddress,uint32 nonce)
    **STep 2**
      Solana: 

  **4. wrapped token**

      | Token        |   Solana Address             |      Polygon address |
      |:---------------------:|:-------------------:|:-------------------:|
      |  AKRE  |  TqnaKWnG1Tgrqq2LfZepca6cPmTmQSCVHAAsNLgZ2aj    | 0xE9c21De62C5C5d0cEAcCe2762bF655AfDcEB7ab3 |
      |  kWh   | TqnaKWnG1Tgrqq2LfZepca6cPmTmQSCVHAAsNLgZ2aj     | 0x5740A27990d4AaA4FB83044a6C699D435B9BA6F1 |
   

**+ Links**

  | Useful Link        |   Useful Link URL            |  
  |:---------------------:|:-------------------:|
  |  Solana Mainnet  |  https://explorer.solana.com/     |
  |  Solana Testnet | https://explorer.solana.com/?cluster=testnet       |
  |  Solana Devnet | https://explorer.solana.com/?cluster=devnet       |
  |  AREC Demo  | https://arec-sol-demo.vercel.app       |
  |  All on-chain program  | https://explorer.solana.com/address/7fEvnVYgDkZfT6JkffusC5f2vcRRMdd6dZqAAWURek61?cluster=devnet     |
  |  How to Verify a Program  | https://solana.com/developers/guides/advanced/verified-builds     |
  |  Intro to client-side Anchor development  | https://solana.com/developers/courses/onchain-development/intro-to-anchor-frontend     |
  |  Anchor-ping Example  | https://github.com/solana-developers/anchor-ping-frontend     |
  |  密钥文件           | E:\BlockchainWallet\Argon\solana22\*.json      |
  |  wormhole-sdk-ts    | E:\BlockchainWallet\Argon\wormhole\wormhole-sdk-ts    |
  |  generate-keypair    | E:\BlockchainWallet\Argon\Solana\generate-keypair    |


**+ Generate Keypair Commands**

```
  E:\BlockchainWallet\Argon\Solana\generate-keypair\generate-keypair.ts
  npx esrun generate-keypair.ts 
  npx esrun check-balance.ts
  npx esrun airdrop.ts
  npx esrun create-token-mint.ts
  npx esrun mint-token_1.ts (X)

  npx esrun wallets.ts
  npx esrun transfer.ts
  npx esrun mints.ts
  npx esrun create-metaplex-collection.ts
```
  
**+ Critical Addresses**

  | Useful Link        |   Address            |                     |
  |:---------------------:|:-------------------:|:-------------------:|
  |  AREC Bridge                |  7fEvnVYgDkZfT6JkffusC5f2vcRRMdd6dZqAAWURek61       |        |
  |  AREC State                 |  4Bz3gpTZ8KgaUdUXCqPcmR1dxcFxVYNd3V3g146EHhGS       |        |
  |  User Arec State            |  HKvC7EshiLQC5qMY5dpD8iq1VkH6wCLZEJuNYH7QTaJb       |        |
  |  Arec Nft Info              |  47Y1q5Zrv64RNAQZsfx86qYGjgMBf5MEHE1oUTUubFKy       |        |
  |  Arec Asset info            |  1goc2wSQjxHjJg6aQtgPGJmMh7SYcEW5KLWwwLtHWi2        | ART Asset Info: issue price..      |
  |  AKRE Token                 |  akreF6MMz2A9safhSdrdyoeWzhHCzNPggJaaY2Npvo4        |        |
  |  Arec Income Account        |  79xyrmkYvvAZDKdetZSS6ox7nCDfz4NCjuhKNxXcYHgx       |        |
  |  User Payment Account       |  G4QbyrhBpPYdUPpJWWUsFwAhtD5hcjDkFUvoGCFa4HJN       |        |
  |  AREC NFT                   |  arec5aj8j6nZB5EZX1jspWRyZh7GiAW4CfN26L6GTNp        |        |
  |  Arec Nft Account           |  ECM2wzUF62qczS65fMFxAUsBT4tQwGzvtWJyku3nuYmL       |        |
  |  AKRE Token                 |  akreF6MMz2A9safhSdrdyoeWzhHCzNPggJaaY2Npvo4        |        |
  |  AREC NFT                   |  arec5aj8j6nZB5EZX1jspWRyZh7GiAW4CfN26L6GTNp        |        |
  |  ART Token                  |  art8zaVhaKBZp6sVeVd72oQoKseFqwNDcxGW32VBe1Q        |        |
  |  Badge NFT                  |  badgeWgrqhK8aHvQuy61gzDo5wHBmqVat8tW3w6qcjg        |        |
  |  Arec Liquidized List       |  2qYEHj698SkSdLqDtWCCvu1BoTdxG1kcC42mTYVeiT9a       |        |
  |  Arec Redeemed List         |  DZHnQkJ4DRMtSbkyNoVYVVosxQ26jFX4bQuzEty2pnhj       |        |
  |  Arec Badge List            |  6N4WaK3niNP7UQTACyhdjNW8kqa2UVTTM685GYyshiJT       |        |
  |  Arec Liquidized Account    |  A8Hf5kh5jcgLqvN95Bboc4dB8yvDvNjPDWzLn4R1eEY3       |        |
  |  Arec Redeemed Account      |  FbjRBkAVk1pH7BMEHEfXYmSVs5YZjjzevJRf5ky2L7c        |        |
  |  Arec Offset Badge Account  |  FRVHLBr3vWoBtmbiMuMAFN6hhoHip4WmayzfsuWBqG4a       |        |
  |  MVP1                       | 9DcHReaSPqt2iFhKZxNY4SjucYNyaYfAKazhHV4XGANa        |  Linux 1  |
  |  MVP2                       | AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc        |  Linux 2  |
  |  MVP3                       | DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz        |  Linux 3 (Devnet Authority) |
  |  MVP4                       | JDqWcKxEmzCHKw2TrANV7QcJP678RWWPMz6pSLYopwmW        |  Linux 4 (AKRE Owner)  |
  |  MVP5                       | 5Qf1GdXUYJgDVK8KPDe28fcSpUruHE3daBF8wrEwf1oc        |  Edge 4  |

  arecAssetInfoAccount:   1goc2wSQjxHjJg6aQtgPGJmMh7SYcEW5KLWwwLtHWi2
  artTokenMint:           art8zaVhaKBZp6sVeVd72oQoKseFqwNDcxGW32VBe1Q
  arecNftMint:            arec5aj8j6nZB5EZX1jspWRyZh7GiAW4CfN26L6GTNp
  climateBadgeMint:       badgeWgrqhK8aHvQuy61gzDo5wHBmqVat8tW3w6qcjg
  arecLiquidizedList:     2qYEHj698SkSdLqDtWCCvu1BoTdxG1kcC42mTYVeiT9a
  arecRedeemedList:       DZHnQkJ4DRMtSbkyNoVYVVosxQ26jFX4bQuzEty2pnhj
  arecBadgeList:          6N4WaK3niNP7UQTACyhdjNW8kqa2UVTTM685GYyshiJT

**+ Wallet List** 

  + Edge (inside...)

    | Useful Link        |   Address            |                     |
    |:---------------------:|:-------------------:|:-------------------:|
    |  Edge 1 |  9gNjtfH461XJXxKDcjnkUpfkofsvSytZVNpy3QCLigke      |  |
    |  Edge 2 |  8rYXr3GiTMnX2Ek4vhJLKTxEmEStuD3nNNrvr8hGBniS      |  |
    |  Edge 3 |  8v3fsEv6UomcAeqcyEf2TdsBff9woYyipgZy3HkFfxqz      |  |
    |  Edge 4 |  5Qf1GdXUYJgDVK8KPDe28fcSpUruHE3daBF8wrEwf1oc      |  |
    |  Edge 5 |  GGh4NnLF5iEJn7AsAVS5izsq2njZKzK9nFEcKNKkcSPs      |  AREC Deploy (Mainnet) |
    |  Edge (WormHole) |  53NfDaRW8BduDLi9pVStJt2cb5mhr4QA8VFsvK1JiNdV      |  Imported |

  + Linux (Leopard...)
    | Useful Link        |   Address            |                     |
    |:---------------------:|:-------------------:|:-------------------:|
    |  Linux 1 |  9DcHReaSPqt2iFhKZxNY4SjucYNyaYfAKazhHV4XGANa      |  |
    |  Linux 2 |  AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc      |  |
    |  Linux 3 |  DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz      |  |
    |  Linux 4 |  JDqWcKxEmzCHKw2TrANV7QcJP678RWWPMz6pSLYopwmW      |  |
    |  Linux 5 |  5Qf1GdXUYJgDVK8KPDe28fcSpUruHE3daBF8wrEwf1oc      |   |


+ Cost to load Program
  + 22wEL63FeAngtByix1GmEV1AjdwGzq29hrdyHtxcCbG4Cq3guwx3cPKzkQcT6GGYZHLuXtKAEXMafoJQ6Tez86RW (System Program: Create Account)
    + 8mtywsEkVd7NFXStiMF1PXQL9GNCsErWChkpXznMJSXm ◎6.01982232  (864781 Bytes)
  + 5pkE694YJ34kFuBWB7hpPdVt8eWEU1MuCSimw7FepWizD7eiUXmy4e9Dudp2F68o1UvjYMhf8XPSmTGcbP7RaGzL (BPF Upgradeable Loader: Upgrade)
    + CVphs2C48sNFAE9bCdZacpBMwy3A6WL4dVJmLFua39XL ◎7.09711896 (1019573 Bytes)

**+ Steps to init AREC**
1. Initalize AREC on-chain program
    + "Arec Init" -> "Initalize AREC on-chain program"
    + xzBDteoYd2bmtbBCsUcY1r5nMDnWu4obH6wrNhPDc6LLP97s7U3ABjtcckRJfgaz6EZ2Jr14WvkWSpfyhiXng12
      + Instruction 1: init_arec
      + Instruction 2: init_arec_list
2. Initalize AREC account A
    + "Arec Init" -> "Initalize AREC account A"
    + 43s7XftooRirvrJFgGQ6wUbjbavHGC3WZVBbyJ1ExSFtuGDZaekQhbGiiNCN2dVcCu3KhoCqjdSRGx8rQVKXNoP
      + Instruction 1: init_arec_account_a
3. Initalize AREC account B
    + "Arec Init" -> "Initalize AREC account B"
    + 5zKR9XF9gzPEhLYcpcafZVgd7U73r5LUJpgN8qUzRx1zfR4fPHmEGPkfeHBYLHWHWPSRPGNRWwF2xbcM52nSbJnv
      + Instruction 1: init_arec_account_b
4. Manage MVP Account
    + "Arec Init" -> "Manage MVP Account"
    + 2LmaoJKu4X8Emish6FS8E6vxmbQKPkgKFb6TGE8jRPAQRk1ZV44SsKCkbbVHVpp2HpfqXqDNR3smpycBDyJUy9ya
      + Instruction 1: manage_mvp
        Add MVP:
        + 9DcHReaSPqt2iFhKZxNY4SjucYNyaYfAKazhHV4XGANa
        + AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc
        + DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz
        + JDqWcKxEmzCHKw2TrANV7QcJP678RWWPMz6pSLYopwmW
        + 5Qf1GdXUYJgDVK8KPDe28fcSpUruHE3daBF8wrEwf1oc
5. Add new AREC Asset
    + "Arec Init" -> "Add new AREC Asset"
    + 4FCutVgZu2a68pry1ve98FRKwb2UazuGtVTQexg7MNh3R7o4uYhVCUVjKpTYvQ4YP3byoSPSPNW2LvxxiD3w9dW5
      + Instruction 1: new_arec_asset
6. Intialize AREC User Account （DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "AREC Bridge" -> "Intialize AREC User Account"
    + 2tQ7RNYmYRQ48jmi8d55bWLLqXEjbcH128XBoNnqyJWWkWp8C2XsfQys6pTeqjaXfPm5qeMaWa9VUwSoX7DZQQrR
      + Instruction 1: init_arec_user

        | Useful Link        |   Address            |                     |
        |:---------------------:|:-------------------:|:-------------------:|
        |  User Account               |  DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz       |        |
        |  AREC State                 |  4Bz3gpTZ8KgaUdUXCqPcmR1dxcFxVYNd3V3g146EHhGS       |        |
        |  User Arec State            |  HKvC7EshiLQC5qMY5dpD8iq1VkH6wCLZEJuNYH7QTaJb       |  各种NFT数量及发电量   |
        |  Arec Nft Mint              |  arec5aj8j6nZB5EZX1jspWRyZh7GiAW4CfN26L6GTNp       |        |
        |  Arec Nft Account           |  ECM2wzUF62qczS65fMFxAUsBT4tQwGzvtWJyku3nuYmL       |        |
        |  Climate Badge Mint         |  badgeWgrqhK8aHvQuy61gzDo5wHBmqVat8tW3w6qcjg       |        |
        |  Climate Badge Account      |  3mJ915ZmK99YzBTYVUabZHhJFi1cDYMhCDzG6DTbXfxF       |        |
7.A Bridge AREC Asset
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 5tKBheyZASeLVcUyhma9iBF8Fn4Yao7967UFiiSMHvq1fkifcY7fSn1cnSh7pFeLpL7iG2Wme6Ns1boi6keoX9gZ
      + Instruction 1: bridge_arec (id = 1)

7.B Bridge AREC Asset
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 2r7Y8756v9SfBrBrTnRfbs9LTwLhKgS6DCKPUamAkZahNifWALi9HKSqt5cpzvQnxEZ92KWycqaKkbyXKRNRvn91
      + Instruction 1: bridge_arec (id = 2)

7.C Bridge AREC Asset
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 5buGcNeWckF7BiXViu6CybBm3Nv4vahWTvUmQQok6bWwEWj3u9xFDT2VWYKkGv8JHPnA5z8hp7SK9NFUSEmGwK9A
      + Instruction 1: bridge_arec (id = 3)

7.D Bridge AREC Asset
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 5onfbbL8fXN4WJewtr1zvhhoqsGoDaMBGB9oL8xkaCTxbSEoc812kZtzHuynmUq6iRqkpBC1sJyUSWjPYVMgjzqb
      + Instruction 1: bridge_arec (id = 4)

7.E Bridge AREC Asset
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 41iqXfK52m6CaDBe8NrUYoKrTfxPaGUSn2LsZkx5Cpn7CYqWdEF4GwvjHGvHS1HgdeMiCaHrQPFARMmsJK41Sisj
      + Instruction 1: bridge_arec (id = 5)

8. Intialize AREC User Account (9DcHReaSPqt2iFhKZxNY4SjucYNyaYfAKazhHV4XGANa)
    + "AREC Bridge" -> "Intialize AREC User Account"
    + BcsMpatY3Kwr1q7cxjcvn2krSvvFqHSCCU45NagJEbxZAPncaCMDcPuBtHRpbE6JwYGY53mDe4V2HWksuHgmQVf
      + Instruction 1: init_arec_user

9. Intialize AREC User Account (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "AREC Bridge" -> "Intialize AREC User Account"
    + 3zhs5Usq9YPe1oVuUHnUzXnSMSV76iVReZLDMjQSZSdkWwf3o18i5DZEmbEBUf8JMVu8riQ4vPLT51K4f37bZ8jZ
      + Instruction 1: init_arec_user
      + Instruction 2: bridge_arec (id = 6)

10. Update_AREC Data (DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "AREC Update" -> "Update AREC asset details"
    + 3MrdX17poa2L2w6a3BGgHnHgPRXXBCVkyWyBQjjpgTumf7Hpv5VwQdpaAz5NQfwWakwvP4Zw1wyqWAPLStd67YSA
      + Instruction 1: update_arec_data (id = 4)

11. Update_AREC Data (DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "AREC Update" -> "Update AREC asset details"
    + 2QhtrkfmurXGdku6o6ky2yWhAK4EreiLTyinrUyFxny7pSqFKCvGidY6i7znG9f7eDnP3t6Qu47XhXkyorhANFkw
      + Instruction 1: update_arec_data (id = 5)

12. Certify AREC NFT (JDqWcKxEmzCHKw2TrANV7QcJP678RWWPMz6pSLYopwmW)
    "Certify AREC" -> "Certify AREC NFT"
    + 4f5tBfhEyd7hHLLEkwBR4bUF7gaoeRiv75wmbRnLeNK8iHQzCJZqT6aNcjdK7T1JrJdQ7bM5kF825zikpBTGXKtB
      + Instruction 1: certify_arec (id = 4)

13. Update_AREC Data (DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "AREC Update" -> "Update AREC asset details"
    + 3eE76mME9fNtdAy9iX7XWWqL1WZAEqtYPDTr4AM5XoFmtb9oTyTULcHoQjRoTE8gmDCKmT4nRxVFxX2MerujJTJ4
      + Instruction 1: update_arec_data (id = 1)

13. Update_AREC Data (DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "AREC Update" -> "Update AREC asset details"
    + 4YU9KRaPdNzEZyj5zUrPZdHTeHuzk7P29XiDPVmHN2SPqkrr3j3y6zY35Pt13fwpD5nkkbWwnjybuK2LtPdHkjNd
      + Instruction 1: update_arec_data (id = 3)

14. Update_AREC Data (DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "AREC Update" -> "Update AREC asset details"
    + BTD59yLfH5sEydE383BNL5A3gnBkXRNWCQT1g6WjwZBzXPPQLcni78cjQLd2UwGgAG5HZXh3nRCuoHrriTuUh58
      + Instruction 1: update_arec_data (id = 2)

15. Bridge AREC Asset (DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "AREC Bridge" -> "Intialize AREC User Account"
    + 2iWZxXnBbg4eatBvFTKpXwgB6UM18Cahc6tVYwt7Jc6Vko1HmWc4sKhz2JhpYBnkBPH3XpAZ5TjG4uJxywmEeyaU
      + Instruction 1: bridge_arec (id = 7)

16. Certify AREC NFT (JDqWcKxEmzCHKw2TrANV7QcJP678RWWPMz6pSLYopwmW)
    + "Cerify Arec" -> "Cerify Arec NFT"
    + 2sw19SsyLa6FSDg6ciMroX6Z35r96yx6kk7VkTbwjtZuSmhYxmzdFVxGqv5ZhD6JCFN2fGpFbfpUjHPASwJTB7iU
      + Instruction 1: certify_arec (id = 2)

17. Bridge AREC Asset (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 3Jdu177ZYFWiiUKsCaB6W19G7BKuHtugnUiKU5aymuEQosAqX1qZPJQut9kBpCAcbrv1fvawpHyV5QGss7WwkbRR
      + Instruction 1: bridge_arec (id = 8)

18. Bridge AREC Asset (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 22AzfrJkwTUqgQ89BRJ2SfXfFdV7kbDshzjqJywqNVvsFyPqVgdQwuYwnvRMya4p3oprH5Y614qRVHwAwmEdq1cz
      + Instruction 1: bridge_arec (id = 9)

19. Liquidize AREC (DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "Liquidize AREC" -> "Liquidize AREC NFT Token"
    + 5xU589CPeBYvbHq6Y7j1xDa1JZxfQWnBw29L2BgzvzpDRcRdxYsejZDYkta6TV5fp5JNTP5mCa6jKD97q7Pov5cZ
      + Instruction 1: liquidize_arec (id = 2)

20. Offset ART (DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "Offset ART -> "Offset ART and mint badge"
    + qCyq6Wnj2hC25r61ZfAsbWTToTPeA4zpXfhq6NktSitvKs3Py7XEQjTdyFQ5xHCvoKcY4Z59qHy5u3anH7KQa2x
      + Instruction 1: offset_arec_badge

21. Offset ART (DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "Offset ART -> "Offset ART and mint badge"
    + 4c7X7KnaXWeK34PJd8huu6bP9sp1UKA9yB6AYaV5QHckBb6sSfRsrqxynMrgZ2kTx2SpXsC7aonVKUdN5Nyq8nV2
      + Instruction 1: offset_arec_badge

22. Offset ART (DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "Offset ART -> "Offset ART and mint badge"
    + 38wNCBEiSZugT5FZ5HGqv71ZwP7AVPsUNW9CxJpWuQARNetHu6mF79wcKfgjaaecqVxS332mSzTmjkoGH1ZaC2cs
      + Instruction 1: offset_arec_badge

23. Bridge AREC Asset (DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz)
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 5BtJXX9S8myeALJqMZxiuBUGeMLZbLKDrEg7Uq61rrXhFutbD3JXFkiDSf8Quf3yQ36pAJU3JfLXxQds8vCoj8qM
      + Instruction 1: bridge_arec (id = 10)

24. Bridge AREC Asset (9DcHReaSPqt2iFhKZxNY4SjucYNyaYfAKazhHV4XGANa)
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 3ouuaLRxQXzCi9icmzfnBABLCBqfVXaoz8Pn9GGLpLP3PeEottyxkYHCtYtmLnBWLWnwCy67H9Qw91VvvSHkDJBQ
      + Instruction 1: bridge_arec (id = 11)

25. Update_AREC Data (9DcHReaSPqt2iFhKZxNY4SjucYNyaYfAKazhHV4XGANa)
    + "AREC Update" -> "Update AREC asset details"
    + 2wMvYSQMN9do6U3Nxy19vXEC3Xskmn7uRUsE8tRodHgenKCQTDXjiHb5VxWwrJiJTNufFQ9ffWqbtviG8cNsreHJ
      + Instruction 1: update_arec_data (id = 11)

26. Bridge AREC Asset (9DcHReaSPqt2iFhKZxNY4SjucYNyaYfAKazhHV4XGANa)
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 2vjY1FSfwjxaa65BMgWikf2AmDBa5Pt7hKFboBYYvvL3MBbgLJRLx4VoC4wfx9ibetH9myzBKQ8762rtScJJ7b72
      + Instruction 1: bridge_arec (id = 12)

27. Bridge AREC Asset (9DcHReaSPqt2iFhKZxNY4SjucYNyaYfAKazhHV4XGANa)
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 2yMjkDYA5XtBg9wb6Q5ud15wvbS2jXnqDVUubkUq3rdC6Z61W7Wr2vbvjn7QMkdjRg2rHp1pqGzcee7zgoYwZTxr
      + Instruction 1: bridge_arec (id = 13)

28. Bridge AREC Asset (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 55hqhFhX1A4mgo6zPkkcX2iLvm6t2eJvJS2h1ceZstmzsCGJGHJT6Rh6bHvAFeQZcB8RvLCviC9rpg6oka2S2kJH
      + Instruction 1: bridge_arec (id = 14)

29. Update_AREC Data (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "AREC Update" -> "Update AREC asset details"
    + 5faaACudPwhLXgMFtXzADqNdmxDBWmzLSgzQB3HQB8DxkoocKJmz4RcdcmchhMGDJcRVHbmtqCTTSQPdS9ATFGzQ
      + Instruction 1: update_arec_data (id = 8)

30. Certify AREC NFT (JDqWcKxEmzCHKw2TrANV7QcJP678RWWPMz6pSLYopwmW)
    + "Cerify Arec" -> "Cerify Arec NFT"
    + 2865C7SVdYfjnPVE8RHea8qnsmmFgWPSu1o1voWNxzsBqeFbFDq1JwYX4cB2NzypuVkSiqzNhrDQtwpJeEp7aLWg
      + Instruction 1: certify_arec (id = 3)

31. Bridge AREC Asset (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 3ja7zhkB1UgAiAU1xGzue2QETxSgt9JX64mt6NvMzSvHoDKSxnLAsVVd7SoHYRBDwvC9kZraFWDe6oXh37wrR19i
      + Instruction 1: bridge_arec (id = 15)

32. Bridge AREC Asset (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "AREC Bridge" -> "Bridge AREC Asset"
    + H4zZ3Y6HLARLgpuVqAHYuFPgUkUXH8NbajtiGachJAZhgBDEGCiH9cTG8ikyxYkw98BFL5iCUqLgExoP76Hft6r
      + Instruction 1: bridge_arec (id = 16)

33. Bridge AREC Asset (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "AREC Bridge" -> "Bridge AREC Asset"
    + 2Jfy9VxJ1Bo6Dk2VMKGHqpf2Nsh3G4YHdpzoYwGmVabRETDjJvRgmUtPd1pQoryTF3c5zdaQZYdmUs3eaUxsDFLg
      + Instruction 1: bridge_arec (id = 17)

34. Update_AREC Data (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "AREC Update" -> "Update AREC asset details"
    + 419aE6wGNTSNYgzBGHNNm8Je3yFW4BfNC3cTHJYV3LsM8k8ZFpGwBu89Ufvxm1v2eRFSqVdWdGDNKyHExUznWUJf
      + Instruction 1: update_arec_data (id = 16)

35. Update_AREC Data (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "AREC Update" -> "Update AREC asset details"
    + AUT6xPWhEKKdgqiADGawUqpKNKC5T1hqgF38dr6SY7E7kEipiXZL8qGagBftnDHtube28eNP5S32xDMxXjmWE3t
      + Instruction 1: update_arec_data (id = 14)

36. Certify AREC NFT (JDqWcKxEmzCHKw2TrANV7QcJP678RWWPMz6pSLYopwmW)
    + "Cerify Arec" -> "Cerify Arec NFT"
    + 1r6zs7AFWAbJ4xFNki6y1kT8YY48gkbU4AyJkXepkotKUk559BcFB6iMqmYzozTRjXPVaq6jXKrYYVebc1NesU4
      + Instruction 1: certify_arec (id = 14)

37. Certify AREC NFT (JDqWcKxEmzCHKw2TrANV7QcJP678RWWPMz6pSLYopwmW)
    + "Cerify Arec" -> "Cerify Arec NFT"
    + Zp6f1TSudCgPcn5U6SxCGZz98pv4tr5QSFk61J5LTafKjuGh9zDzP9EdGQYHbViQcMM3fCMozhrBPyyU1891zMa
      + Instruction 1: certify_arec (id = 16)

38. Liquidize AREC (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "Liquidize AREC" -> "Liquidize AREC NFT Token"
    + 3q8mpydEtJR4KiEA7SeZbA62d1UWQ8NE6Tace9xMhPwawRc3DRNsjKyM24xRXTriqM7ZP8NoEAwfCWSFqGuQD4EV
      + Instruction 1: liquidize_arec (id = 16)

39. Liquidize AREC (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "Liquidize AREC" -> "Liquidize AREC NFT Token"
    + 2L2yGV5MFJKsK8AhFxFVAcyLyG5w3tLsLyUx957qjSUXQsht5XjCceKbhpsg7jJo52qnjc3RT4taoP4UJoFf6Cog
      + Instruction 1: liquidize_arec (id = 14)

40. Offset ART (AcyVq43dVqHPpXbCmP7jZ2K59GYtdb2yCjkrxAn9PvFc)
    + "Offset ART -> "Offset ART and mint badge"
    + 5M7NtupWSp7NU5XHZPM37C85Re8fHzmcxSehCV7EsMS8CnaQ6AkEkBfB1uy2TvpGYYJZgrEQx1nA3EcMqMt91nKy
      + Instruction 1: offset_arec_badge

**+ How to Verify On-Chain Program**
  + https://github.com/Ellipsis-Labs/solana-verifiable-build
  + https://github.com/neodyme-labs/solana-security-txt


**+ How to setup Solana development environment**

```
  Status: No Curl, Node, yarn, npm, git

  1. sudo apt install curl 

  2. How to install nodejs
    # installs nvm (Node Version Manager)
    a. curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
        a.1 close and open terminal again

    # download and install Node.js (you may need to restart the terminal)
    b. nvm install 20
        nvm install 18
        nvm install 22
    
    # verifies the right Node.js version is in the environment
    c. node -v # should print `v20.16.0`
        v20.17.0
    
    # verifies the right npm version is in the environment
    d. npm -v # should print `10.8.1`
        10.8.2

  3. How to install yarn:  
    (https://stackoverflow.com/questions/53471063/yarn-error-there-are-no-scenarios-must-have-at-least-one)
    a. sudo apt remove yarn 	(skip)
    b. curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
      -> Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
      -> OK
    c. echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
      -> deb https://dl.yarnpkg.com/debian/ stable main
    d. sudo apt update && sudo apt install yarn
    e. yarn --version
        1.22.22
        
  4. sudo apt install git 	(Must)   
    -> git --version
        git version 2.34.1
        git version 2.25.1 (ubuntu 20)
    
  5. Install rust
    a. curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh  
        -> 1) Proceed with standard installation (default - just press enter)
        -> close and reopen
        
        
    -> Rust is installed now. Great!

    -> To get started you may need to restart your current shell.
    -> This would reload your PATH environment variable to include
    -> Cargo's bin directory ($HOME/.cargo/bin).

    -> To configure your current shell, you need to source
    -> the corresponding env file under $HOME/.cargo.

    -> This is usually done by running one of the following (note the leading DOT):
    -> . "$HOME/.cargo/env"            # For sh/bash/zsh/ash/dash/pdksh
    -> source "$HOME/.cargo/env.fish"  # For fish
        
    b. rustup --version
        -> rustup 1.27.1 (54dd3d00f 2024-04-24)
    c. rustup install 1.79.0
    d. rustup show
    e. rustup default 1.79.0-x86_64-unknown-linux-gnu     
    
  6. Install solana-cli:
    (https://docs.solanalabs.com/cli/install)
    a. sh -c "$(curl -sSfL https://release.solana.com/v1.18.18/install)"
        sh -c "$(curl -sSfL https://release.solana.com/v1.17.22/install)"    (use this version)

      -> Adding 
      -> export PATH="/home/ldru/.local/share/solana/install/active_release/bin:$PATH" to /home/ldru/.profile
      -> Close and reopen your terminal to apply the PATH changes or run the following in your existing shell:
      -> export PATH="/home/ldru/.local/share/solana/install/active_release/bin:$PATH"

      b. export PATH="/home/ldru/.local/share/solana/install/active_release/bin:$PATH" to /home/ldru/.profile
            -> Close and reopen your terminal to apply the PATH changes or run the following in your existing shell:
                export PATH="/home/ldru/.local/share/solana/install/active_release/bin:$PATH"
            ** Close and reopen your terminal
            
          b.1 If have problem, add following line to the file  /home/ldru/.bashrc
              export PATH="/home/ldru/.local/share/solana/install/active_release/bin:$PATH"

    c. sudo apt-get install build-essential pkg-config libudev-dev llvm libclang-dev protobuf-compiler
      (Must install to solve the error "linker `cc` not found")   
      
    d. solana --version
            ->  solana-cli 1.17.22 (src:dbf06e25; feat:3580551090, client:SolanaLabs)

  7. How to install anchor: (https://www.anchor-lang.com/docs/installation)
      a. cargo install --git https://github.com/coral-xyz/anchor avm --locked --force
        ->  Installed package `avm v0.30.1 (https://github.com/coral-xyz/anchor#7cb20f25)` (executables `anchor`, `avm`)
      b. avm list
      c. avm install 0.30.1
        ->  warning: be sure to add `/home/ldru/.avm/bin` to your PATH to be able to run the installed binaries
            Now using anchor version 0.30.1.
      d. export PATH="/home/ldru/.avm/bin:$PATH"
      e. echo $PATH
      f. anchor --version
        ->  anchor-cli 0.30.1
        
  8. https://stack.vesocial.com/solution/problem-with-anchor-build-says-my-active-rustc-version-is-1      


  9. solana-keygen new
    -> Generating a new keypair
    -> For added security, enter a BIP39 passphrase
    -> NOTE! This passphrase improves security of the recovery seed phrase NOT the
    -> keypair file itself, which is stored as insecure plain text
    -> BIP39 Passphrase (empty for none): 
    -> Wrote new keypair to /home/ldru/.config/solana/id.json
    -> ===========================================================================
    -> pubkey: JDqWcKxEmzCHKw2TrANV7QcJP678RWWPMz6pSLYopwmW
    -> ===========================================================================
    -> Save this seed phrase and your BIP39 passphrase to recover your new keypair:
    -> voyage .... census
    -> ===========================================================================
    
  10.  How to generate ssh key:
    ** ssh-keygen -t ed25519 -C "ludaoru@gmail.com" 
    -> Your identification has been saved in /home/ldru/.ssh/id_ed25519
    -> Your public key has been saved in /home/ldru/.ssh/id_ed25519.pub

```

**+  Good.txt**
      
```
  9gNjtfH461XJXxKDcjnkUpfkofsvSytZVNpy3QCLigke
  8rYXr3GiTMnX2Ek4vhJLKTxEmEStuD3nNNrvr8hGBniS
  8v3fsEv6UomcAeqcyEf2TdsBff9woYyipgZy3HkFfxqz

  2024/10/07:


  2024/10/05:

  anchor test --skip-deploy

  solana config set --url devnet
  solana-keygen recover -o arec.json --force
  solana program deploy --buffer arec.json /home/ldru/solana/ArkreenSol/target/deploy/arec_sol.so
  anchor deploy -- --max-sign-attempts 10000 --with-compute-unit-price 10000

  solana program extend 7fEvnVYgDkZfT6JkffusC5f2vcRRMdd6dZqAAWURek61 200000


  Recover the intermediate account's ephemeral keypair file with
  `solana-keygen recover` and the following 12-word seed phrase:
  =============================================================================
  sea wheel cart orbit motor mandate street kangaroo where illness crawl animal
  =============================================================================
  To resume a deploy, pass the recovered keypair as the
  [BUFFER_SIGNER] to `solana program deploy` or `solana program write-buffer'.
  Or to recover the account's lamports, pass it as the
  [BUFFER_ACCOUNT_ADDRESS] argument to `solana program close`.
  =============================================================================
  Error: 385 write transactions failed
  There was a problem deploying: Output { status: ExitStatus(unix_wait_status(256)), stdout: "", stderr: "" }.

  solana program extend 7fEvnVYgDkZfT6JkffusC5f2vcRRMdd6dZqAAWURek61 200000

  -u d -k ./authority_keypair.json 


  Where -u is the rpc url or moniker (d for devnet in this example) -k the path to the program upgrade authority keypair (signer) 20000 is 20 kb more space, adjust properly. And prog111111111111111111111111111111111111111 should be your deployed program id. – 
  kevinrodriguez-io
  CommentedMar 18 at 23:25 


  SSSSSSSSSSS arec5aj8j6nZB5EZX1jspWRyZh7GiAW4CfN26L6GTNp 
  A8Hf5kh5jcgLqvN95Bboc4dB8yvDvNjPDWzLn4R1eEY3 FbjRBkAVk1pH7BMEHEfXYmSVs5YZjjzevJRf5ky2L7c FRVHLBr3vWoBtmbiMuMAFN6hhoHip4WmayzfsuWBqG4a


  DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz
  init-data-access.tsx:53 SSSSSSSSSSSSSSS arec5aj8j6nZB5EZX1jspWRyZh7GiAW4CfN26L6GTNp A8Hf5kh5jcgLqvN95Bboc4dB8yvDvNjPDWzLn4R1eEY3 FbjRBkAVk1pH7BMEHEfXYmSVs5YZjjzevJRf5ky2L7c FRVHLBr3vWoBtmbiMuMAFN6hhoHip4WmayzfsuWBqG4a

    Bridging AREC asset
  SSSSSSSSSSS 
  DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz 
  arec5aj8j6nZB5EZX1jspWRyZh7GiAW4CfN26L6GTNp 
  A8Hf5kh5jcgLqvN95Bboc4dB8yvDvNjPDWzLn4R1eEY3 
  FbjRBkAVk1pH7BMEHEfXYmSVs5YZjjzevJRf5ky2L7c 
  FRVHLBr3vWoBtmbiMuMAFN6hhoHip4WmayzfsuWBqG4a 
  11111111111111111111111111111111 
  TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb

  SSSSSSSSSSSSSSS 
  DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz 
  arec5aj8j6nZB5EZX1jspWRyZh7GiAW4CfN26L6GTNp 
  A8Hf5kh5jcgLqvN95Bboc4dB8yvDvNjPDWzLn4R1eEY3 
  FbjRBkAVk1pH7BMEHEfXYmSVs5YZjjzevJRf5ky2L7c 
  FRVHLBr3vWoBtmbiMuMAFN6hhoHip4WmayzfsuWBqG4a 
  11111111111111111111111111111111 
  TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb


  2024/10/05:
  sudo mkdir /mnt/shared
  sudo mount -t vboxsf shares /mnt/shared

  npx create-solana-dapp@latest

  2024/09/12:

  Require, Revert, and Custom Errors in Solana:
  https://www.rareskills.io/post/solana-require-macro

  2024/09/10:
  Set git editor to VSCode:
  git config --global core.editor "code --wait"
  git config --local --list

  git branch -M main
  git remote add origin git@github.com:Lu-Derik/arec-sol-demo.git
  git push -u origin main


  2024/09/05:

  https://solana.com/developers/courses/token-extensions/group-member  (!!!!!!!!!!!!!!!!!)

  https://hackernoon.com/how-to-mint-solana-nft-using-anchor-and-metaplex
  https://medium.com/@elchuo160/create-your-own-on-chain-nfts-on-solana-with-anchor-and-quicknode-a-step-by-step-guide-2024-c108077013e9

  https://solana.stackexchange.com/questions/5047/anchor-initialize-token-mint-with-name-and-symbol (!!!!!!!!!!!)


  2024/09/03:

  https://www.quicknode.com/guides/solana-development/anchor/token-2022 (!!!!!!!!!!!!)

  https://www.quicknode.com/guides/solana-development/anchor/how-to-use-constraints-in-anchor

  https://github.com/coral-xyz/anchor/tree/v0.30.0/tests/spl/token-extensions
  https://spl.solana.com/token-2022/onchain


  solana-keygen pubkey target/deploy/my_program-keypair.json

  solana-keygen pubkey /home/ldru/solana/spl_token-extensions/target/deploy/token_extensions-keypair.json


  https://medium.com/web3-builders-alliance/local-validator-test-your-program-directly-from-your-pc-c66397b00bdf (!!!!!!!!!!!!!)

  1. mkdir ~/.local/share/valid8 (OK)
  2. solana program dump -u m metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s ~/.local/share/valid8/metadata.so (OK)
  3. sudo nano /usr/local/bin/metaplex-test-validator

  #!/bin/bash

  # Validator command
  COMMAND="solana-test-validator -r --bpf-program metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s ~/.local/share/valid8/metadata.so"

  # Append any additional arguments passed to the script
  for arg in "$@"
  do
      COMMAND+=" $arg"
  done

  # Execute the command
  eval $COMMAND

  4. sudo chmod +x /usr/local/bin/metaplex-test-validator


  5. metaplex-test-validator 			(!!!!!!!!!!!!!!!!)
  6. anchor test --skip-local-validator		(!!!!!!!!!!!!!!!!!!!!)
  7. solana-test-validator --reset



  2024//09/02
  https://github.com/helium/helium-program-library

  2024//09/01

  https://gateway.irys.xyz/C93vAsk0FannhNsubXyN2-6ZqR9_XSaLTY58zSAi4Fw
  https://gateway.irys.xyz/AfC010ous5ij95SAjGE-LKi-bP2-X2lBBhxldM1P-zs

  https://gateway.irys.xyz/qDewOi6QR837_OFHC45HCSpKpJaMzp6_nEuxsZMk0aU
  https://gateway.irys.xyz/5VhTD-t9WOyQcTCvM1TjMjpjJpoqt4rhdaFDkzPC0yc

  rimraf node_modules
  yarn cache clean

  2024//08/30

  Upgrade Authority:                    DKfM6YcF2wXDSCUMLP6LamkTwvVRpHdCj6n69gmYGQJz
  Program Executable Data Account:      AhZ5YcQ5z52UyHQcV4BzAZZngdSpvKm2ktykTHmKgc3j
                                        346429 Bytes: ◎2.41203672

  anchor upgrade target/deploy/<PROGRAM_NAME>.so --provider.cluster <CLUSTER> --program-id <PROGRAM_ID>

  2024/08/29:
  Full-stack Solana development with React and Anchor:
  https://solana.com/developers/guides/getstarted/full-stack-solana-development

  Program Derived Address (PDA):
  https://solana.com/docs/core/pda#breadcrumbs

  How to CPI with a PDA Signer in a Solana program:
  https://solana.com/developers/guides/getstarted/how-to-cpi-with-signer


  https://solana.com/developers/guides/getstarted/how-to-cpi-with-signer


  1. anchor keys list
  2. anchor keys sync
  3. solana config get
  4. solana balance
  5. solana address
  6. solana airdrop 5
  7. solana program close --buffers

  #######################################
  2024/08/28

  1. 安装指定的 Solana CLI 版本:
    solana-install init 1.18.0
    solana-install init 1.17.22
      ->  ✨ 1.18.0 initialized
  2.  solana --version
    -> solana-cli 1.18.0 (src:b1e37800; feat:1836278484, client:SolanaLabs)

  3. 清除 yarn 缓存: 
      yarn cache clean
  4.  npm cache clean --force


  #######################################

  1. Net setting:
  DevNet: https://api.devnet.solana.com
  TestNet: https://api.testnet.solana.com
  MainNet: https://api.mainnet-beta.solana.com

  2. solana config set --url https://api.testnet.solana.com
    solana config set --url https://api.devnet.solana.com
    solana config set --url http://127.0.0.1:8899
    
    solana transfer 9DcHReaSPqt2iFhKZxNY4SjucYNyaYfAKazhHV4XGANa 10000 --allow-unfunded-recipient
    
    ldru@ldru:~$    solana transfer 9DcHReaSPqt2iFhKZxNY4SjucYNyaYfAKazhHV4XGANa 10000
  Error: The recipient address (9DcHReaSPqt2iFhKZxNY4SjucYNyaYfAKazhHV4XGANa) is not funded. Add `--allow-unfunded-recipient` to complete the transfer 
  ldru@ldru:~$ 


  3. solana config get
  Config File: /Users/you/.config/solana/cli/config.yml
  RPC URL: https://api.devnet.solana.com
  WebSocket URL: wss://api.devnet.solana.com/ (computed)
  Keypair Path: /Users/you/.config/solana/id.json
  Commitment: confirmed

  4. solana-keygen new -o /mnt/e/BlockchainWallet/Argon/solana22/test_wallet.json
  5. solana config set --keypair /mnt/e/BlockchainWallet/Argon/solana22/test_wallet.json
  6. spl-token create-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb --enable-close
    -> Address:  RNWwsTN9Qri4rV2p5CWGAsfGC7AEd9nvaX8L9K5KRbb
  7. spl-token display RNWwsTN9Qri4rV2p5CWGAsfGC7AEd9nvaX8L9K5KRbb
    ->  SPL Token Mint
          Address: RNWwsTN9Qri4rV2p5CWGAsfGC7AEd9nvaX8L9K5KRbb
          Program: TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
          Supply: 0
          Decimals: 9
          Mint authority: DveG63nc2CW5dEtiyNN9oxkaHvtkwj327zTaJN4RGyst
          Freeze authority: (not set)
        Extensions
          Close authority: DveG63nc2CW5dEtiyNN9oxkaHvtkwj327zTaJN4RGyst
  8. spl-token close-mint RNWwsTN9Qri4rV2p5CWGAsfGC7AEd9nvaX8L9K5KRbb
  9. spl-token create-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
    ->  Address:  2A9P6ehr1exTLYNybVWL2r3JbWrMguSqgf6rZJkJVquV
        Decimals:  9
  10. spl-token create-account 2A9P6ehr1exTLYNybVWL2r3JbWrMguSqgf6rZJkJVquV
    ->  Creating account 46z6xnTXLobpNFtkodR5zNBHTfqGSA7hqFmEGxp2r5wE
  11. spl-token mint 2A9P6ehr1exTLYNybVWL2r3JbWrMguSqgf6rZJkJVquV 1000
    ->  Minting 1000 tokens
        Token: 2A9P6ehr1exTLYNybVWL2r3JbWrMguSqgf6rZJkJVquV
        Recipient: 46z6xnTXLobpNFtkodR5zNBHTfqGSA7hqFmEGxp2r5wE
  12. spl-token display 2A9P6ehr1exTLYNybVWL2r3JbWrMguSqgf6rZJkJVquV 
    ->  SPL Token Mint
          Address: 2A9P6ehr1exTLYNybVWL2r3JbWrMguSqgf6rZJkJVquV
          Program: TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
          Supply: 1000000000000
          Decimals: 9
          Mint authority: DveG63nc2CW5dEtiyNN9oxkaHvtkwj327zTaJN4RGyst
          Freeze authority: (not set)
  13. spl-token create-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb --decimals 0 --enable-metadata --enable-non-transferable        
    ->  Creating token BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX under program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
        To initialize metadata inside the mint, please run `spl-token initialize-metadata BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX <YOUR_TOKEN_NAME> <YOUR_TOKEN_SYMBOL> <YOUR_TOKEN_URI>`, and sign with the mint authority.

        Address:  BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX
        Decimals:  0
  14. spl-token initialize-metadata BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX ARECTestToken ATKTest http://arec.arkreen.com
  15. spl-token display BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX 
    ->  SPL Token Mint
          Address: BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX
          Program: TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
          Supply: 0
          Decimals: 0
          Mint authority: DveG63nc2CW5dEtiyNN9oxkaHvtkwj327zTaJN4RGyst
          Freeze authority: (not set)
        Extensions
          Non-transferable
          Metadata Pointer:
            Authority: DveG63nc2CW5dEtiyNN9oxkaHvtkwj327zTaJN4RGyst
            Metadata address: BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX
          Metadata:
            Update Authority: DveG63nc2CW5dEtiyNN9oxkaHvtkwj327zTaJN4RGyst
            Mint: BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX
            Name: ARECTestToken
            Symbol: ATKTest
            URI: http://arec.arkreen.com
  16. spl-token update-metadata BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX asset-type "classic bridged REC"
    ->  ...
        Metadata:
        Update Authority: DveG63nc2CW5dEtiyNN9oxkaHvtkwj327zTaJN4RGyst
        Mint: BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX
        Name: ARECTestToken
        Symbol: ATKTest
        URI: http://arec.arkreen.com
        asset-type: classic bridged REC
  17. spl-token update-metadata BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX asset-type --remove
  18. spl-token update-metadata BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX "Asset Type" "Classic Bridged REC"
    ->  ...
        Metadata:
        Update Authority: DveG63nc2CW5dEtiyNN9oxkaHvtkwj327zTaJN4RGyst
        Mint: BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX
        Name: ARECTestToken
        Symbol: ATKTest
        URI: http://arec.arkreen.com
        Asset Type: Classic Bridged REC
  19. spl-token create-account BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX
    ->  Creating account H5fhkWKcFLicZBNyprdeVXL869NRAx6CeDDbzaNYAgTs
  20. spl-token mint BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX 1
    ->  Minting 1 tokens
        Token: BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX
        Recipient: H5fhkWKcFLicZBNyprdeVXL869NRAx6CeDDbzaNYAgTs
  21. spl-token authorize BTT2yKP2ZaupXt7DPT7MaJF3dEAWxCsm4vuniVfjctwX mint --disable      
  #################################

  Solana22:
  1. curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
    -> 关闭窗口, 并重新打开

  2. nvm --version
    -> 0.40.0

  3. node -v
    -> v20.17.0

  4. npm -v
    -> 10.8.2

  5. yarn -v
    -> 1.22.19

  6. git --version
    -> git version 2.34.1

  7. Install rust
    a. curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
      -> 1  (Default)
      -> To configure your current shell, you need to source
        the corresponding env file under $HOME/.cargo.
        
        This is usually done by running one of the following (note the leading DOT):
        . "$HOME/.cargo/env"            # For sh/bash/zsh/ash/dash/pdksh
        source "$HOME/.cargo/env.fish"  # For fish

    b. rustup --version
        ->  rustup 1.27.1 (54dd3d00f 2024-04-24)
            info: This is the version for the rustup toolchain manager, not the rustc compiler.
            info: The currently active `rustc` version is `rustc 1.80.1 (3f5fd8dd4 2024-08-06)`

    c. rustup install 1.79.0
        ->  1.79.0-x86_64-unknown-linux-gnu installed - rustc 1.79.0 (129f3b996 2024-06-10)

    d. rustup show
        ->  Default host: x86_64-unknown-linux-gnu
            rustup home:  /home/ldru/.rustup

            installed toolchains
            --------------------

            stable-x86_64-unknown-linux-gnu (default)
            1.79.0-x86_64-unknown-linux-gnu

            active toolchain
            ----------------

            stable-x86_64-unknown-linux-gnu (default)
            rustc 1.80.1 (3f5fd8dd4 2024-08-06)

    e. rustup default 1.79.0-x86_64-unknown-linux-gnu
        ->  info: using existing install for '1.79.0-x86_64-unknown-linux-gnu'
            info: default toolchain set to '1.79.0-x86_64-unknown-linux-gnu'

            1.79.0-x86_64-unknown-linux-gnu unchanged - rustc 1.79.0 (129f3b996 2024-06-10)

    f. rustup show
        ->  Default host: x86_64-unknown-linux-gnu
            rustup home:  /home/ldru/.rustup
            
            installed toolchains
            --------------------
            
            stable-x86_64-unknown-linux-gnu
            1.79.0-x86_64-unknown-linux-gnu (default)
            
            active toolchain
            ----------------
            
            1.79.0-x86_64-unknown-linux-gnu (default)
            rustc 1.79.0 (129f3b996 2024-06-10)          

  8. Install solana-cli: (https://docs.solanalabs.com/cli/install)
    a. sh -c "$(curl -sSfL https://release.solana.com/v1.18.18/install)"
      sh -c "$(curl -sSfL https://release.solana.com/v1.17.22/install)"
      ->  downloading v1.18.18 installer
          ✨ 1.18.18 initialized
          Adding
          export PATH="/home/ldru/.local/share/solana/install/active_release/bin:$PATH" to /home/ldru/.profile

          Close and reopen your terminal to apply the PATH changes or run the following in your existing shell:

          export PATH="/home/ldru/.local/share/solana/install/active_release/bin:$PATH"
      -> 关闭窗口, 并重新打开

    b. sudo apt-get update (必须先执行)

    c. sudo apt-get install build-essential pkg-config libudev-dev llvm libclang-dev protobuf-compiler
        (Must install to solve the error "linker `cc` not found")

    d. solana --version
      ->  solana-cli 1.18.18 (src:83047136; feat:4215500110, client:SolanaLabs)


  9. How to install anchor: (https://www.anchor-lang.com/docs/installation)
      a. cargo install --git https://github.com/coral-xyz/anchor avm --locked --force
        ->  Installed package `avm v0.30.1 (https://github.com/coral-xyz/anchor#7cb20f25)` (executables `anchor`, `avm`)
      b. avm list
      c. avm install 0.30.1
        ->  warning: be sure to add `/home/ldru/.avm/bin` to your PATH to be able to run the installed binaries
            Now using anchor version 0.30.1.
      d. export PATH="/home/ldru/.avm/bin:$PATH"
      e. echo $PATH
      f. anchor --version
        ->  anchor-cli 0.30.1
      
  10. solana-keygen new
      ->  Generating a new keypair
          For added security, enter a BIP39 passphrase

          NOTE! This passphrase improves security of the recovery seed phrase NOT the
          keypair file itself, which is stored as insecure plain text

          BIP39 Passphrase (empty for none):

          Wrote new keypair to /home/ldru/.config/solana/id.json
          ======================================================================
          pubkey: BKFhMFPKJNCjkogDQkVZ1YrPCAbbTqKs6uVzGgjwx5YP
          ======================================================================
          Save this seed phrase and your BIP39 passphrase to recover your new keypair:
          sea ... trick
          ======================================================================

  11. anchor init sol-arec
  12. cd sol-arec
  13. anchor build

  14. Add following to Anchor.toml (Must)
      [test]
      startup_wait = 20000

  15. anchor test   (OK) 

  #################################

  1. sudo apt install curl 

  2. How to install nodejs
    # installs nvm (Node Version Manager)
    a. curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash

    # download and install Node.js (you may need to restart the terminal)
    b. nvm install 20
        nvm install 18
        nvm install 22
    
    # verifies the right Node.js version is in the environment
    c. node -v # should print `v20.16.0`
    
    # verifies the right npm version is in the environment
    d. npm -v # should print `10.8.1`

  3. WSL重新安装yarn:
    https://stackoverflow.com/questions/53471063/yarn-error-there-are-no-scenarios-must-have-at-least-one
    a. sudo apt remove yarn
    b. curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
    c. echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
    d. sudo apt update && sudo apt install yarn
    e. yarn --version
        1.22.22

  4. 启动 VirtualBox 需要关闭 "虚拟机平台"
    "cmd" -> "windows features"

  5. Install Rust
    a. 显示已安装版本:
      rustup show
    b. 显示可安装版本：
      rustup target list
    c. 安装指定版本:  
      rustup install 1.79
    d. 切换到指定版本:  
      rustup default 1.79-x86_64-pc-windows-msvc (Windows)

      apt-get install build-essential pkg-config libudev-dev llvm libclang-dev protobuf-compiler

  6. Install rust
    a. curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh  
    b. rustup --version
    c. rustup install 1.79.0
    d. rustup show
    e. rustup default 1.79.0-x86_64-unknown-linux-gnu

  7. Install solana-cli:
    (https://docs.solanalabs.com/cli/install)
    a. sh -c "$(curl -sSfL https://release.solana.com/v1.18.18/install)"
    b1. export PATH="/Users/ldru/.local/share/solana/install/active_release/bin:$PATH" to /Users/you/.profile (Must)
        (Adding export PATH="/Users/you/.local/share/solana/install/active_release/bin:$PATH" to /Users/you/.profile)
  
    b2. export PATH="/home/ldru/.local/share/solana/install/active_release/bin:$PATH" (Not recommend)
    c. sudo apt-get install build-essential pkg-config libudev-dev llvm libclang-dev protobuf-compiler  (Must)
      (Must install to solve the error "linker `cc` not found")
    
  8. How to install anchor:
    (https://www.anchor-lang.com/docs/installation)
    a. cargo install --git https://github.com/coral-xyz/anchor avm --locked --force
        (error: linker `cc` not found) solved by 7.c 
    b. avm list
    c. avm install 0.30.1
        warning: be sure to add `/home/ldru/.avm/bin` to your PATH to be able to run the installed binaries
      Now using anchor version 0.30.1.
    d. export PATH="/home/ldru/.avm/bin:$PATH"
    e. echo $PATH

    https://explorer.solana.com/tx/4iaz31nHRA3SqsEF7yKvz866VdAsdPqovKgUftmGu3QHF77Yd9KdG6ZQgkoMe1AQ5K8SzyyKnkU5hXUrsJgryxuH?cluster=devnet


  ###################################
  9.    https://solana.com/developers/courses/tokens-and-nfts
  10.   https://solana.com/developers/guides/games/interact-with-tokens
  11.   https://developers.metaplex.com/
  12.   https://beta.solpg.io/tutorials/battle-coins
  12.A 	https://beta.solpg.io/65ace254cffcf4b13384cf14

  13.   https://www.quicknode.com/guides/solana-development/anchor/create-tokens

  14.   https://beta.solpg.io/

  https://solana.com/developers/guides/getstarted/scaffold-nextjs-anchor
  https://solana.stackexchange.com/questions/13408/could-not-find-pda-and-state-in-mpl-token-metadata

  https://solana.com/developers/courses/intro-to-solana (O)
  https://solana.com/developers/courses/tokens-and-nfts (3)
  https://solana.com/developers/courses/onchain-development (O)
  https://solana.com/developers/courses/token-extensions (O)
  https://solana.com/developers/courses/program-optimization (O)
  https://solana.com/developers/courses/state-compression (2)
  https://solana.com/developers/courses/program-security (O)
  https://solana.com/developers/courses/mobile (3)
  https://solana.com/developers/courses/offline-transactions  (O)
  https://solana.com/developers/courses/solana-pay (O)

  https://solana-labs.github.io/solana-web3.js/

  #########################
  https://solana-labs.github.io/solana-web3.js/
  https://faucet.solana.com/
  @solana/wallet-adapter-base
  @solana/wallet-adapter-react
  @solana/wallet-adapter-react-ui
  https://github.com/wallet-standard/wallet-standard
  https://github.com/solana-developers/create-solana-dapp

  https://github.com/Unboxed-Software/solana-ping-frontend/tree/starter
  https://github.com/Unboxed-Software/solana-ping-frontend

  https://github.com/solana-labs/dapp-scaffold (OK)
  https://github.com/solana-labs/wallet-adapter#usage

  https://anza-xyz.github.io/wallet-adapter/example/

  https://beta.solpg.io/

  https://www.anchor-lang.com/
  https://medium.com/@qiaopengjun0/solana-%E5%BC%80%E5%8F%91%E5%AD%A6%E4%B9%A0%E4%B9%8Bsolana-%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86-7faf849d8f9c
  https://www.solanazh.com/course/7-2
  https://solana.com/developers/guides/getstarted/setup-local-development
  https://code.visualstudio.com/docs/remote/wsl-tutorial
  https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer
  https://solana.com/docs/clients/javascript-reference
  https://solana.com/developers/courses
  1. https://solana.com/developers/courses/intro-to-solana/intro-to-cryptography
  ... https://solana.com/developers/courses/intro-to-solana/intro-to-reading-data

  https://developers.metaplex.com/token-metadata  

  Solana Playground
  https://beta.solpg.io/

  https://solana-labs.github.io/solana-web3.js/

  https://docs.rs/anchor-lang/latest/anchor_lang/

  C:\Users\lenovo\.local\share\solana\install\releases\1.18.18\solana-release

  https://www.solanazh.com/assets/files/web3-ui-demo.zip
  https://www.solanazh.com/assets/files/wallet-adapter-demo.zip
  https://www.solanazh.com/assets/files/spl-token-demo.zip
  https://www.solanazh.com/assets/files/spl-token-exercise.zip

  Unified Token List API:
  https://github.com/solflare-wallet/utl-api

  NFT metadata
  https://lsc6xffbdvalb5dvymf5gwjpeou7rr2btkoltutn5ij5irlpg3wa.arweave.net/XIXrlKEdQLD0dcML01kvI6n4x0GanLnSbeoT1EVvNuw


  Metaplex JavaScript SDK README 
  https://github.com/metaplex-foundation/js

  Metaplex JS SDK Examples:
  https://github.com/metaplex-foundation/js-examples

  Solana NFT standard:
  https://developers.metaplex.com/token-metadata/token-standard#the-non-fungible-standard

  Certified Collection i
  https://developers.metaplex.com/token-metadata/collections
    

```      

**+  Deployment Transaction List**

```
4thwKiMbvEmpkrnkdX7N3NYaVRiFoyzgSnnnUiXcGgnB3GMoFPHosbSB7dUL…
332,886,336	3 months ago	Oct 14, 2024 at 14:49:43 UTC	Success
3vKiRCtNXD9MjoGowLgjpyMXiFzTBfafWKEpyNgigec3qbtDZhq5Laskt1tb…
332,353,908	3 months ago	Oct 12, 2024 at 07:29:35 UTC	Success
7fNa8VJsYxB8qoBoEGgmNNJxbG2NXusg48uPEqDcxE9h24aRDsmyGHhrSaku…
332,353,818	3 months ago	Oct 12, 2024 at 07:29:02 UTC	Success
fYYPfi8SVCyAx4oPu1eFnZRvx6jhWYYJHFL9B8TsnR7HTBtJSkBG7PFQH8NW…
332,353,565	3 months ago	Oct 12, 2024 at 07:27:27 UTC	Success
5WaDVQ1MpY7WH2EjeqrBTJf6hKX1V99VBpzZ3HgLoAM4AeijHhpKZdNzoAHW…
332,352,428	3 months ago	Oct 12, 2024 at 07:20:21 UTC	Success
3DZYPZfXSKy6DwJ9iX36QeAxbjaiQE2N9Bw8mVnyHpBRSv43Vfgxf77bu1hy…
332,352,007	3 months ago	Oct 12, 2024 at 07:17:45 UTC	Success
5BtJXX9S8myeALJqMZxiuBUGeMLZbLKDrEg7Uq61rrXhFutbD3JXFkiDSf8Q…
331,959,564	3 months ago	Oct 10, 2024 at 14:37:45 UTC	Success
38wNCBEiSZugT5FZ5HGqv71ZwP7AVPsUNW9CxJpWuQARNetHu6mF79wcKfgj…
331,926,372	3 months ago	Oct 10, 2024 at 11:11:37 UTC	Success
4c7X7KnaXWeK34PJd8huu6bP9sp1UKA9yB6AYaV5QHckBb6sSfRsrqxynMrg…
331,926,312	3 months ago	Oct 10, 2024 at 11:11:15 UTC	Success
qCyq6Wnj2hC25r61ZfAsbWTToTPeA4zpXfhq6NktSitvKs3Py7XEQjTdyFQ5…
331,925,776	3 months ago	Oct 10, 2024 at 11:07:57 UTC	Success
5xU589CPeBYvbHq6Y7j1xDa1JZxfQWnBw29L2BgzvzpDRcRdxYsejZDYkta6…
331,882,192	3 months ago	Oct 10, 2024 at 06:37:31 UTC	Success
2iWZxXnBbg4eatBvFTKpXwgB6UM18Cahc6tVYwt7Jc6Vko1HmWc4sKhz2Jhp…
331,843,828	3 months ago	Oct 10, 2024 at 02:39:10 UTC	Success
BTD59yLfH5sEydE383BNL5A3gnBkXRNWCQT1g6WjwZBzXPPQLcni78cjQLd2…
331,843,747	3 months ago	Oct 10, 2024 at 02:38:39 UTC	Success
4YU9KRaPdNzEZyj5zUrPZdHTeHuzk7P29XiDPVmHN2SPqkrr3j3y6zY35Pt1…
331,843,520	3 months ago	Oct 10, 2024 at 02:37:15 UTC	Success
3eE76mME9fNtdAy9iX7XWWqL1WZAEqtYPDTr4AM5XoFmtb9oTyTULcHoQjRo…
331,841,648	3 months ago	Oct 10, 2024 at 02:25:38 UTC	Success
2QhtrkfmurXGdku6o6ky2yWhAK4EreiLTyinrUyFxny7pSqFKCvGidY6i7zn…
331,684,936	3 months ago	Oct 9, 2024 at 10:14:55 UTC	Success
3MrdX17poa2L2w6a3BGgHnHgPRXXBCVkyWyBQjjpgTumf7Hpv5VwQdpaAz5N…
331,684,659	3 months ago	Oct 9, 2024 at 10:13:11 UTC	Success
41iqXfK52m6CaDBe8NrUYoKrTfxPaGUSn2LsZkx5Cpn7CYqWdEF4GwvjHGvH…
331,413,296	3 months ago	Oct 8, 2024 at 06:14:02 UTC	Success
5onfbbL8fXN4WJewtr1zvhhoqsGoDaMBGB9oL8xkaCTxbSEoc812kZtzHuyn…
331,412,830	3 months ago	Oct 8, 2024 at 06:11:10 UTC	Success
5buGcNeWckF7BiXViu6CybBm3Nv4vahWTvUmQQok6bWwEWj3u9xFDT2VWYKk…
331,411,680	3 months ago	Oct 8, 2024 at 06:04:06 UTC	Success
2r7Y8756v9SfBrBrTnRfbs9LTwLhKgS6DCKPUamAkZahNifWALi9HKSqt5cp…
331,271,696	3 months ago	Oct 7, 2024 at 15:39:46 UTC	Success
5tKBheyZASeLVcUyhma9iBF8Fn4Yao7967UFiiSMHvq1fkifcY7fSn1cnSh7…
331,234,994	3 months ago	Oct 7, 2024 at 11:48:59 UTC	Success
4RsJ4Gzw2ucwLbMPGrD4ddsT9uWYEB1CqeZcYpqwzwS9vFqTsxXf8UP2RbHA…
331,234,880	3 months ago	Oct 7, 2024 at 11:48:16 UTC	Success
2tQ7RNYmYRQ48jmi8d55bWLLqXEjbcH128XBoNnqyJWWkWp8C2XsfQys6pTe…
331,233,280	3 months ago	Oct 7, 2024 at 11:38:10 UTC	Success
5pkE694YJ34kFuBWB7hpPdVt8eWEU1MuCSimw7FepWizD7eiUXmy4e9Dudp2…  :  Upgrade
331,193,352	3 months ago	Oct 7, 2024 at 07:25:51 UTC	Success
...
22wEL63FeAngtByix1GmEV1AjdwGzq29hrdyHtxcCbG4Cq3guwx3cPKzkQcT…   :
331,193,088	3 months ago	Oct 7, 2024 at 07:24:11 UTC	Success
```


**Vanity Address**

```
2025/1/14

Swap:
The public key is:  gBtcc5o7TGyG7PRWVMipoCqSLsGrtko3CfbQamAL7Qp
The secret key is:  Uint8Array(64) [
  206, 176, 158, 154,  51,  46, 184, 252, 93,  83, 196,
  246,  94,  76, 207, 185, 237, 189, 122, 99,   8,  77,
   56, 235,  76, 142, 216, 116, 185, 165, 98, 109,  10,
    9, 246, 252, 236, 154, 231, 211,  28, 58, 147, 153,
  157,   3,  71,  90,  45, 202, 149, 242, 89,   6, 173,
  135, 171,   8, 148, 117,  87, 223,  76,  5
]

GreenBTC:
Index: 14750000
The public key is:  GBTCvvVMubu8S64sjauXMjWPPWzTg7DZnHtY1PAMdv37
The secret key is:  Uint8Array(64) [
  102,  64,  14,   1, 134,  74,  20, 249, 113,  52, 125,
  197,  29,  97,  36, 108, 109, 189, 173, 242, 206, 209,
  235,  56, 116, 126,   9, 239, 127, 243,  62,  65, 225,
  140, 190,  43,  70,  80,  75, 101, 213, 123,  87,  64,
  218, 221,  97, 175, 190, 212,  41, 180, 152, 131, 104,
  106, 190,  84,  61, 208,  58, 182,  44, 238
]
Index: 14760000



The public key is:  usdTvp4sHSStYhaDRZEYgju14Gyu7mAvTqMguddqZnr
The secret key is:  Uint8Array(64) [
  192, 178, 134, 170, 125, 177,  86,  11, 234, 158, 114,
  252, 242, 192, 227,  46,  74, 120, 182,  19, 179, 188,
  215, 243,  89, 125,  24, 142, 185, 253, 237, 107,  13,
  139, 114, 183, 239,   0, 133, 239,  81, 116, 117,  25,
    2, 134,  29,  52, 243,  26,  75, 180, 253, 157, 101,
  149, 173, 254, 169, 165, 225,  84,  41, 163
]
The public key is:  UsDTRTaSpN3jvXy5a2KJA1TCN6PLhh7voU6g1xmgfLh
The secret key is:  Uint8Array(64) [
  197,  86,  41,  78, 130,  23, 168, 220,   8, 162, 206,
   98, 139,  48,  36,  32, 219,  53,   7,  68, 151, 180,
  137,  62, 102, 176,  99, 102, 158, 114,  35,  74,   7,
   35, 117, 184,  98, 254,  58, 233, 205, 166, 163, 244,
  181, 118,  22, 232, 101,   9, 104,  76, 151,  15, 155,
  224, 228, 119,  77,  86,  18,  75, 244, 134
]

The public key is:  UsdTvSLQKYMRh4V9cyFziXC16Ftim7mAZBk3oAPVPAy
The secret key is:  Uint8Array(64) [
  252,  64, 199, 142,  95, 110,  27,  20,  27, 222,  59,
  247,  76,  56, 155,   4,  13, 255, 107,  81,  26, 238,
  136,  84,  97,  20,  35,  84, 181, 201,  86, 241,   7,
   35, 237, 138,  51, 231, 105, 200,  23, 234, 173, 109,
  222, 218, 211,  53, 150,  43,  24, 211,  92, 249, 216,
  110, 225,  15, 240, 107,  39, 160,  45,  58
]

The public key is:  KWhfC6nWAefvH9Yy23xfichPWPtkhtgURE7d7y5oXHf
The secret key is:  Uint8Array(64) [
  203, 178, 127, 217, 251,  66, 196, 226, 151, 200, 246,
  195, 208,  88, 157, 178, 183, 156,  67, 182, 165, 153,
  170, 162, 130, 154,  68, 139,  28, 147, 235,  74,   4,
  190,   9, 160,  44, 160, 252, 201, 239,  96, 137, 166,
  235, 150, 221,  10, 106,  51, 224, 131,  75, 194,   9,
   23,  55, 213,   1, 220, 155, 159,  47, 238
]
The public key is:  0 kwhHz1GKrUchtLbxocXmmh2UZSUuT17io2auveaUBmB
The secret key is:  Uint8Array(64) [
  180, 164, 156, 118, 183, 184, 149, 124, 216, 214,  74,
  191, 231,  71,  82,  37, 152,  74,  83,  64, 154, 142,
   75,  15, 153,  31, 191, 194,  58, 183, 221, 148,  11,
   65, 209, 123,  94, 167, 211,   4, 212, 194, 135, 111,
   96,  76, 175,  18, 184, 249, 191, 207, 120, 119, 210,
  247,  42,  76, 105, 112, 126, 210, 135,  18
]
Index: 1300000
The public key is:  KwHJJ1jCyn1GcTiYsg5TPdXFjWqSKEh9DQJAyRUZnL8
The secret key is:  Uint8Array(64) [
  251,  57, 180,  33, 131, 142, 112, 203,  59, 229,  7,
  195,  66, 120, 150,  74, 235, 177,  66,  94,  65, 16,
  105, 134,  87,   7, 143, 115, 210, 222, 107, 169,  4,
  217, 212, 141, 207, 106, 211,  93, 238, 167,   9, 67,
  104, 249, 190, 194,  45, 246,  18, 198, 200, 123, 34,
   45, 149,  31, 190, 154,  46,  96, 115, 217
]
Index: 1400000
Index: 1500000
Index: 1600000
Index: 1700000
The public key is:  KwH4SFmogpEaxpisWmKjoCTcdNcxSNWT4Q7pkw7UoAZ
The secret key is:  Uint8Array(64) [
   30, 206, 233, 137, 142,  17, 185, 228, 230, 193,   9,
   67, 131,  60,  76,  21, 227, 195, 187, 153,  44,  33,
   52, 144,  23,  65, 226,   3,  63, 124, 156,  58,   4,
  217, 211,  92, 140, 217,   1, 168, 241, 234,  16, 161,
   58, 247, 188, 230,  10, 172, 231, 222, 199, 240,  63,
  227,  43,  36,   1, 145,  24,  53,  65,  58
]
Index: 1800000
The public key is:  KWh4KjKeXfZZALrW3GbUKkEXtkUHSWBXoLYBgV4HTpU
The secret key is:  Uint8Array(64) [
   41, 142, 201,  98, 125, 211, 113, 170,  40, 224,  81,
  222,   7, 246, 204, 188, 160, 177,  61,  36,  72,   0,
   37,  79,  22, 170, 207,  50, 102,  20,  10, 227,   4,
  190,   6, 160,  24, 166,  32,  30, 130, 148, 213,  81,
  233, 167, 203, 140, 234,  29,  57, 124,  92, 132, 103,
  251, 111,  28, 116, 132, 111, 167,  25,  89
]
The public key is:  1 KWHobG1zEG9HM2FaEx6k7szwxuxVK7qk2TXc73YzuK9
The secret key is:  Uint8Array(64) [
  168, 115, 107, 160,  71, 212,  45, 117,  89, 221, 219,
   91, 193, 232,  23, 223, 107, 143, 181, 118,  97,  52,
  235,  63, 146,  79,  54, 212, 117, 112, 159,  79,   4,
  189, 146, 146,  97, 253, 176, 219,  16,  12, 204, 234,
  220,  98, 158,  33,  28, 142,  93,  70, 243, 212,  44,
  108,  15, 123,   8,  77, 182, 192, 213, 132
]
The public key is:  kWHrAVNePt1Mh3jHfYxtgbXcXPQdoExYWbY6gBZu6bt
The secret key is:  Uint8Array(64) [
  124, 198,  67,  41, 246,  87, 235, 183,  46, 232, 242,
   12, 110, 151,  44,  26, 181, 228, 150, 220,  30, 171,
   39, 165, 119,  38,  17,  58, 231, 113, 124, 143,  11,
   37,  23, 248, 165, 204,  78, 231, 224, 198,  44,  95,
   47, 198, 177, 226,  88,  54,  23,  67, 210, 207,   1,
  201, 121, 186, 154, 142,   5, 147,  43,  59
]
Index: 2700000
The public key is:  KWhuNgTRBZdamsRjadQNHpofW2gYFVVmuvdqFrZxt2T
The secret key is:  Uint8Array(64) [
   31,  64, 199, 119,  20, 173, 132, 176, 219, 254, 129,
   46,  87,  36, 210, 177,  82, 105, 153,  76,  89, 200,
  171, 131,  91, 198,  11,  92, 145,  57, 106, 240,   4,
  190,  10, 216, 149,  67,  45, 215, 116,   8, 137,  26,
   65, 139,  47,  11, 104,  73,  86, 194,  43,  28, 154,
  108,  82, 168, 246,  19, 236,  40, 168,  56
]
The public key is:  2 kwhg4nxqgPCZWZYAY67CVGGGXHCzhvvbUhVusF1aEbk
The secret key is:  Uint8Array(64) [
  197,  31,  69,  53,  77, 246,  52, 183, 190, 145, 116,
   88,  60, 242, 255, 111,  47,   8, 108, 173, 123,  95,
    6, 227,  91, 122,   8, 189, 102,  65, 133, 216,  11,
   65, 211,  97, 205,  49,  57, 211,  90, 100, 202,  58,
  240,  54, 104, 102, 197, 218, 250, 216,  35, 140,  53,
    6, 206, 222, 255,   3, 132, 248,  51,  27
]
The public key is:  KWhTj7QSYA3oz3x8RDSJn8esR5PWvWauKmNuPEU1ozT
The secret key is:  Uint8Array(64) [
   42, 246,  22, 112,  63, 247, 161, 209,  26, 146, 145,
   38, 170, 121,  14, 207, 253, 232,   2, 240, 199,  32,
  255, 237, 175, 203, 176,   3, 215, 174,  90, 166,   4,
  190,   8, 163, 158,  10,   1, 201, 116, 101, 164, 190,
   78, 215, 223,  80,  28,  12, 119, 223, 130, 216, 146,
  237, 132, 255,  35, 127,  67, 208,  19, 204
]
The public key is:  kWHSgFPVEuL7NmkVQc59qXkKX4YnLB5rQAEwMuad1k5
The secret key is:  Uint8Array(64) [
    5, 125, 207,  69, 139, 238, 227, 141, 109, 248, 214,
   14,  31, 201, 112, 190, 229, 109, 160, 136, 234,  60,
   40, 129, 171,   1,  92,  77, 100, 185, 154, 151,  11,
   37,  21, 243,  71, 217,  74, 246,   2,  60, 111, 108,
  196,  16, 107, 108, 137,  37, 158, 213, 183,  30, 156,
  210, 177,  29,  35,  64,  46,  76, 249, 242
]
The public key is:  kWHZeHdmd47Nz4CF6Z4SFVrErGW3bD9kr4eJV4E4Dmu
The secret key is:  Uint8Array(64) [
  205,  71,  87, 101,  72, 243, 106, 128,  10, 233,  53,
   44, 243,  45, 152, 214, 187, 162,  21,  40,  60,   8,
   36, 137, 240, 202, 166, 161,  87, 165, 125,  68,  11,
   37,  22, 140, 187,  31, 179, 162,   2, 214,  38,  60,
   73,  83,   9,  70,  94,  18,  14, 164, 140, 198, 240,
   77, 218,  48, 208, 241, 180, 164, 209, 132
]
The public key is:  3 kWh8Rpcc3oozKUTn6FGt26cry5ZwpEgieMexKGWf7Ew
The secret key is:  Uint8Array(64) [
  174, 167,  57,  34,  15, 153,  83,  83,   4, 116, 105,
   43, 112, 159,  12, 108,  56, 239, 116,  36, 108,  52,
   59,  96,  65, 201, 117, 251, 143, 156, 170, 158,  11,
   37, 140,  40,  28,  25,   9, 229,  51, 137,  36, 255,
  226,  56,  46,  11, 190, 112,   2,  88, 197, 141, 191,
  144,  50,  47, 196,  71, 170,  96, 190,  32
]
The public key is:  kwHyrgwQaejfr5vDkbsLDFkJ12rmn7Zqk7yauLzEiyX
The secret key is:  Uint8Array(64) [
   44, 159, 110, 151, 170, 141, 225,   5,  76, 108, 206,
  168, 220,   1, 138,   6, 235, 237,  83, 107, 230, 250,
  108, 195,   6, 238, 114, 226, 223,  20, 179, 244,  11,
   65,  93,  34, 229, 109,   5, 162, 115,  56, 122, 246,
  197, 121,  26, 212, 127,  16, 214, 133,   5, 228, 206,
   47, 206,  84, 205,  95, 232, 142,  62, 138
]


2025/1/14

The public key is:  0 swapXGGphuhMFS8MSXTXSsHhadaE9TG9Ls4MS1wNZC2
The secret key is:  Uint8Array(64) [
  236,  91, 236,  79, 251, 122,   5, 236,  22, 123, 130,
   62,   1, 126, 194,  27,   4, 155, 186,  65, 223, 133,
  193, 146, 235, 245, 128,  80, 222, 169, 201,  59,  13,
   12, 193, 252,  21,  70, 233,  64,  20, 194,  73, 107,
   11, 114, 155, 215,  92, 254,  32,  46, 150,  62,  37,
  107, 216, 104,  71, 217, 255, 213, 142, 231
]

The public key is:  sWaPPooHExHeRbWiL1BtKHH8wLxUQ6mYePmsYQJnJyq
The secret key is:  Uint8Array(64) [
  134, 129,  51,  50,  17, 208, 160, 147,  56, 219,  38,
   28, 190, 102,  99,   2, 249, 242,  11,  25,  31,  61,
  234,  74, 247,  54, 215, 169, 249,  81,  62, 165,  12,
  240, 123,  81, 196, 167, 157, 195,  15, 111, 233, 233,
  104, 120, 197, 190,  75, 225, 204, 183, 170,  63, 252,
   34, 187,  40, 132,  10, 151, 133, 247, 124
]
Index: 71300000

Index: 20400000
Index: 20500000
The public key is:  sWaPYLmK7QrMPy4EqSZ9PagX9NEAhHs8HzZ5aJraD8e
The secret key is:  Uint8Array(64) [
  132, 178, 173, 184,  86,  48,  75, 102,  74,  75, 249,
   43, 241, 236,  57,  40, 156, 179,  96,  57, 249, 115,
  141,  65, 152, 156, 136, 147, 164, 214, 138, 200,  12,
  240, 123,  85,   2,  96,  55,  59, 201, 236, 131, 114,
  151,  37,   0, 120,  23,   1,  95, 174,  56, 171, 226,
  204, 106, 148,  82, 160,  11, 206, 104, 131

Index: 30500000
The public key is:  sWApvzEwVhBjVJBc5gRDMtMRx1SUVCkMQmUCzTxgugm
The secret key is:  Uint8Array(64) [
  252,  45, 225, 155, 101, 111, 77, 151,  77, 240,  92,
  103,  62,  52,  55, 123,  10, 71,  27, 205, 162, 254,
  163, 152, 192, 248, 147,  58, 14,  97, 190, 241,  12,
  240,   5, 189, 127,  49, 233, 46,  17, 177, 131, 131,
  154, 186, 182,  98, 237,  58,  2,  31,  41,  21, 175,
  202, 111, 250, 109, 236,   3, 53,  39, 218
]
Index: 30600000
Index: 30700000
Index: 30800000
Index: 30900000


Index: 67100000
Index: 67200000
The public key is:  SWapHQjhzcAdAqAkJ93SJxJ2qCpZMRh9tge4aNhb144
The secret key is:  Uint8Array(64) [
  133,  59, 150, 101,  99,  39,  37,  32,  94,  67,  71,
   75, 133, 150, 103, 112, 175, 115, 123, 117,  92, 181,
  151, 218, 227,  21, 173, 211, 253, 166,  36, 220,   6,
  136, 248,  72, 114, 104,  46, 116,  11, 145, 195,  92,
   13, 116, 121, 118, 157,  79, 131, 219,  42,  28,   8,
   93,  49, 180, 203, 255,  43, 122, 223,  97
]
Index: 67300000
Index: 67400000
Index: 67500000

The public key is:  swAP1pZTqjjuNExgUJd2FaQ2fDAMMm6adZXpp2KPcdD
The secret key is:  Uint8Array(64) [
  230,  11, 222, 138, 126,  54, 42, 119,  57, 30,   0, 65,
   30,   5, 171,  98,  67, 135, 64, 238,  74, 85, 145, 65,
   81, 145,  87, 147,  46, 133, 26,   0,  13, 12,  72,  3,
  100, 190,  29, 119,  67, 105, 52, 104,  75, 28,  39,  4,
  146, 150,  80,  29,  40, 116, 64, 199, 250, 66,  52, 67,
  150, 139,  45, 144
]
Index: 77700000
Index: 77800000

Swap:
The public key is:  gBtcc5o7TGyG7PRWVMipoCqSLsGrtko3CfbQamAL7Qp
The secret key is:  Uint8Array(64) [
  206, 176, 158, 154,  51,  46, 184, 252, 93,  83, 196,
  246,  94,  76, 207, 185, 237, 189, 122, 99,   8,  77,
   56, 235,  76, 142, 216, 116, 185, 165, 98, 109,  10,
    9, 246, 252, 236, 154, 231, 211,  28, 58, 147, 153,
  157,   3,  71,  90,  45, 202, 149, 242, 89,   6, 173,
  135, 171,   8, 148, 117,  87, 223,  76,  5
]

GreenBTC:
Index: 14750000
The public key is:  GBTCvvVMubu8S64sjauXMjWPPWzTg7DZnHtY1PAMdv37
The secret key is:  Uint8Array(64) [
  102,  64,  14,   1, 134,  74,  20, 249, 113,  52, 125,
  197,  29,  97,  36, 108, 109, 189, 173, 242, 206, 209,
  235,  56, 116, 126,   9, 239, 127, 243,  62,  65, 225,
  140, 190,  43,  70,  80,  75, 101, 213, 123,  87,  64,
  218, 221,  97, 175, 190, 212,  41, 180, 152, 131, 104,
  106, 190,  84,  61, 208,  58, 182,  44, 238
]
Index: 14760000

The public key is:  usdTvp4sHSStYhaDRZEYgju14Gyu7mAvTqMguddqZnr
The secret key is:  Uint8Array(64) [
  192, 178, 134, 170, 125, 177,  86,  11, 234, 158, 114,
  252, 242, 192, 227,  46,  74, 120, 182,  19, 179, 188,
  215, 243,  89, 125,  24, 142, 185, 253, 237, 107,  13,
  139, 114, 183, 239,   0, 133, 239,  81, 116, 117,  25,
    2, 134,  29,  52, 243,  26,  75, 180, 253, 157, 101,
  149, 173, 254, 169, 165, 225,  84,  41, 163
]
The public key is:  UsDTRTaSpN3jvXy5a2KJA1TCN6PLhh7voU6g1xmgfLh
The secret key is:  Uint8Array(64) [
  197,  86,  41,  78, 130,  23, 168, 220,   8, 162, 206,
   98, 139,  48,  36,  32, 219,  53,   7,  68, 151, 180,
  137,  62, 102, 176,  99, 102, 158, 114,  35,  74,   7,
   35, 117, 184,  98, 254,  58, 233, 205, 166, 163, 244,
  181, 118,  22, 232, 101,   9, 104,  76, 151,  15, 155,
  224, 228, 119,  77,  86,  18,  75, 244, 134
]

The public key is:  UsdTvSLQKYMRh4V9cyFziXC16Ftim7mAZBk3oAPVPAy
The secret key is:  Uint8Array(64) [
  252,  64, 199, 142,  95, 110,  27,  20,  27, 222,  59,
  247,  76,  56, 155,   4,  13, 255, 107,  81,  26, 238,
  136,  84,  97,  20,  35,  84, 181, 201,  86, 241,   7,
   35, 237, 138,  51, 231, 105, 200,  23, 234, 173, 109,
  222, 218, 211,  53, 150,  43,  24, 211,  92, 249, 216,
  110, 225,  15, 240, 107,  39, 160,  45,  58
]

The public key is:  UsDrRiXuo6mK5HKYE8K6UFcNJhpCcGDGLpZzgcU3Qzf
The secret key is:  Uint8Array(64) [
  103, 227, 195,   0, 202, 129,  42, 197,  56,  28, 118,
  245,  98,  10, 158, 152,  17, 236,  98,  81,  45,  24,
    0,  96,  15,  24,  51, 222,  72, 205, 182, 215,   7,
   35, 119, 179,  32,  58,  62,  61, 129, 214, 173, 176,
  134,  63, 171, 113, 107, 177, 160, 184, 142, 146, 227,
   20, 167, 154,  23, 240, 109,  68, 249, 108
]

The public key is:  0 usd7xe7UJP37sWk7hNjphy7gig61LAG2bZt4kbqNkpf
The secret key is:  Uint8Array(64) [
  172,  24, 172, 201,  37,  55, 222,  40, 181, 102,  60,
  138, 202,  21,  96, 175, 111, 161, 227, 224, 188, 170,
   77,  80, 109, 212,  90, 166,   9, 175, 109,  44,  13,
  139, 113,   0,  18,   4,  75,  80, 161, 153, 100, 237,
  246,  92, 123, 227, 220, 103, 247,  97, 116,  25, 177,
   84, 197,  49, 150,  66, 171, 199,  86, 160
]

The public key is:  KWhfC6nWAefvH9Yy23xfichPWPtkhtgURE7d7y5oXHf
The secret key is:  Uint8Array(64) [
  203, 178, 127, 217, 251,  66, 196, 226, 151, 200, 246,
  195, 208,  88, 157, 178, 183, 156,  67, 182, 165, 153,
  170, 162, 130, 154,  68, 139,  28, 147, 235,  74,   4,
  190,   9, 160,  44, 160, 252, 201, 239,  96, 137, 166,
  235, 150, 221,  10, 106,  51, 224, 131,  75, 194,   9,
   23,  55, 213,   1, 220, 155, 159,  47, 238
]
The public key is:  0 kwhHz1GKrUchtLbxocXmmh2UZSUuT17io2auveaUBmB
The secret key is:  Uint8Array(64) [
  180, 164, 156, 118, 183, 184, 149, 124, 216, 214,  74,
  191, 231,  71,  82,  37, 152,  74,  83,  64, 154, 142,
   75,  15, 153,  31, 191, 194,  58, 183, 221, 148,  11,
   65, 209, 123,  94, 167, 211,   4, 212, 194, 135, 111,
   96,  76, 175,  18, 184, 249, 191, 207, 120, 119, 210,
  247,  42,  76, 105, 112, 126, 210, 135,  18
]
Index: 1300000
The public key is:  KwHJJ1jCyn1GcTiYsg5TPdXFjWqSKEh9DQJAyRUZnL8
The secret key is:  Uint8Array(64) [
  251,  57, 180,  33, 131, 142, 112, 203,  59, 229,  7,
  195,  66, 120, 150,  74, 235, 177,  66,  94,  65, 16,
  105, 134,  87,   7, 143, 115, 210, 222, 107, 169,  4,
  217, 212, 141, 207, 106, 211,  93, 238, 167,   9, 67,
  104, 249, 190, 194,  45, 246,  18, 198, 200, 123, 34,
   45, 149,  31, 190, 154,  46,  96, 115, 217
]
Index: 1400000
Index: 1500000
Index: 1600000
Index: 1700000
The public key is:  KwH4SFmogpEaxpisWmKjoCTcdNcxSNWT4Q7pkw7UoAZ
The secret key is:  Uint8Array(64) [
   30, 206, 233, 137, 142,  17, 185, 228, 230, 193,   9,
   67, 131,  60,  76,  21, 227, 195, 187, 153,  44,  33,
   52, 144,  23,  65, 226,   3,  63, 124, 156,  58,   4,
  217, 211,  92, 140, 217,   1, 168, 241, 234,  16, 161,
   58, 247, 188, 230,  10, 172, 231, 222, 199, 240,  63,
  227,  43,  36,   1, 145,  24,  53,  65,  58
]
Index: 1800000
The public key is:  KWh4KjKeXfZZALrW3GbUKkEXtkUHSWBXoLYBgV4HTpU
The secret key is:  Uint8Array(64) [
   41, 142, 201,  98, 125, 211, 113, 170,  40, 224,  81,
  222,   7, 246, 204, 188, 160, 177,  61,  36,  72,   0,
   37,  79,  22, 170, 207,  50, 102,  20,  10, 227,   4,
  190,   6, 160,  24, 166,  32,  30, 130, 148, 213,  81,
  233, 167, 203, 140, 234,  29,  57, 124,  92, 132, 103,
  251, 111,  28, 116, 132, 111, 167,  25,  89
]
The public key is:  1 KWHobG1zEG9HM2FaEx6k7szwxuxVK7qk2TXc73YzuK9
The secret key is:  Uint8Array(64) [
  168, 115, 107, 160,  71, 212,  45, 117,  89, 221, 219,
   91, 193, 232,  23, 223, 107, 143, 181, 118,  97,  52,
  235,  63, 146,  79,  54, 212, 117, 112, 159,  79,   4,
  189, 146, 146,  97, 253, 176, 219,  16,  12, 204, 234,
  220,  98, 158,  33,  28, 142,  93,  70, 243, 212,  44,
  108,  15, 123,   8,  77, 182, 192, 213, 132
]
The public key is:  kWHrAVNePt1Mh3jHfYxtgbXcXPQdoExYWbY6gBZu6bt
The secret key is:  Uint8Array(64) [
  124, 198,  67,  41, 246,  87, 235, 183,  46, 232, 242,
   12, 110, 151,  44,  26, 181, 228, 150, 220,  30, 171,
   39, 165, 119,  38,  17,  58, 231, 113, 124, 143,  11,
   37,  23, 248, 165, 204,  78, 231, 224, 198,  44,  95,
   47, 198, 177, 226,  88,  54,  23,  67, 210, 207,   1,
  201, 121, 186, 154, 142,   5, 147,  43,  59
]
Index: 2700000
The public key is:  KWhuNgTRBZdamsRjadQNHpofW2gYFVVmuvdqFrZxt2T
The secret key is:  Uint8Array(64) [
   31,  64, 199, 119,  20, 173, 132, 176, 219, 254, 129,
   46,  87,  36, 210, 177,  82, 105, 153,  76,  89, 200,
  171, 131,  91, 198,  11,  92, 145,  57, 106, 240,   4,
  190,  10, 216, 149,  67,  45, 215, 116,   8, 137,  26,
   65, 139,  47,  11, 104,  73,  86, 194,  43,  28, 154,
  108,  82, 168, 246,  19, 236,  40, 168,  56
]
The public key is:  2 kwhg4nxqgPCZWZYAY67CVGGGXHCzhvvbUhVusF1aEbk
The secret key is:  Uint8Array(64) [
  197,  31,  69,  53,  77, 246,  52, 183, 190, 145, 116,
   88,  60, 242, 255, 111,  47,   8, 108, 173, 123,  95,
    6, 227,  91, 122,   8, 189, 102,  65, 133, 216,  11,
   65, 211,  97, 205,  49,  57, 211,  90, 100, 202,  58,
  240,  54, 104, 102, 197, 218, 250, 216,  35, 140,  53,
    6, 206, 222, 255,   3, 132, 248,  51,  27
]
The public key is:  KWhTj7QSYA3oz3x8RDSJn8esR5PWvWauKmNuPEU1ozT
The secret key is:  Uint8Array(64) [
   42, 246,  22, 112,  63, 247, 161, 209,  26, 146, 145,
   38, 170, 121,  14, 207, 253, 232,   2, 240, 199,  32,
  255, 237, 175, 203, 176,   3, 215, 174,  90, 166,   4,
  190,   8, 163, 158,  10,   1, 201, 116, 101, 164, 190,
   78, 215, 223,  80,  28,  12, 119, 223, 130, 216, 146,
  237, 132, 255,  35, 127,  67, 208,  19, 204
]
The public key is:  kWHSgFPVEuL7NmkVQc59qXkKX4YnLB5rQAEwMuad1k5
The secret key is:  Uint8Array(64) [
    5, 125, 207,  69, 139, 238, 227, 141, 109, 248, 214,
   14,  31, 201, 112, 190, 229, 109, 160, 136, 234,  60,
   40, 129, 171,   1,  92,  77, 100, 185, 154, 151,  11,
   37,  21, 243,  71, 217,  74, 246,   2,  60, 111, 108,
  196,  16, 107, 108, 137,  37, 158, 213, 183,  30, 156,
  210, 177,  29,  35,  64,  46,  76, 249, 242
]
The public key is:  kWHZeHdmd47Nz4CF6Z4SFVrErGW3bD9kr4eJV4E4Dmu
The secret key is:  Uint8Array(64) [
  205,  71,  87, 101,  72, 243, 106, 128,  10, 233,  53,
   44, 243,  45, 152, 214, 187, 162,  21,  40,  60,   8,
   36, 137, 240, 202, 166, 161,  87, 165, 125,  68,  11,
   37,  22, 140, 187,  31, 179, 162,   2, 214,  38,  60,
   73,  83,   9,  70,  94,  18,  14, 164, 140, 198, 240,
   77, 218,  48, 208, 241, 180, 164, 209, 132
]
The public key is:  3 kWh8Rpcc3oozKUTn6FGt26cry5ZwpEgieMexKGWf7Ew
The secret key is:  Uint8Array(64) [
  174, 167,  57,  34,  15, 153,  83,  83,   4, 116, 105,
   43, 112, 159,  12, 108,  56, 239, 116,  36, 108,  52,
   59,  96,  65, 201, 117, 251, 143, 156, 170, 158,  11,
   37, 140,  40,  28,  25,   9, 229,  51, 137,  36, 255,
  226,  56,  46,  11, 190, 112,   2,  88, 197, 141, 191,
  144,  50,  47, 196,  71, 170,  96, 190,  32
]
The public key is:  kwHyrgwQaejfr5vDkbsLDFkJ12rmn7Zqk7yauLzEiyX
The secret key is:  Uint8Array(64) [
   44, 159, 110, 151, 170, 141, 225,   5,  76, 108, 206,
  168, 220,   1, 138,   6, 235, 237,  83, 107, 230, 250,
  108, 195,   6, 238, 114, 226, 223,  20, 179, 244,  11,
   65,  93,  34, 229, 109,   5, 162, 115,  56, 122, 246,
  197, 121,  26, 212, 127,  16, 214, 133,   5, 228, 206,
   47, 206,  84, 205,  95, 232, 142,  62, 138
]

E:\BlockchainWallet\Argon\solana22\ArkreenSol>npx esrun tests/utils/mint-arec-basics.ts
Index: 0
Index: 100000
Index: 200000
Index: 300000
Index: 400000
Index: 500000
Index: 600000
The public key is:  UsDrRiXuo6mK5HKYE8K6UFcNJhpCcGDGLpZzgcU3Qzf
The secret key is:  Uint8Array(64) [
  103, 227, 195,   0, 202, 129,  42, 197,  56,  28, 118,
  245,  98,  10, 158, 152,  17, 236,  98,  81,  45,  24,
    0,  96,  15,  24,  51, 222,  72, 205, 182, 215,   7,
   35, 119, 179,  32,  58,  62,  61, 129, 214, 173, 176,
  134,  63, 171, 113, 107, 177, 160, 184, 142, 146, 227,
   20, 167, 154,  23, 240, 109,  68, 249, 108
]
Index: 700000
Index: 800000
Index: 900000
Index: 1000000
The public key is:  0 usd7xe7UJP37sWk7hNjphy7gig61LAG2bZt4kbqNkpf
The secret key is:  Uint8Array(64) [
  172,  24, 172, 201,  37,  55, 222,  40, 181, 102,  60,
  138, 202,  21,  96, 175, 111, 161, 227, 224, 188, 170,
   77,  80, 109, 212,  90, 166,   9, 175, 109,  44,  13,
  139, 113,   0,  18,   4,  75,  80, 161, 153, 100, 237,
  246,  92, 123, 227, 220, 103, 247,  97, 116,  25, 177,
   84, 197,  49, 150,  66, 171, 199,  86, 160
]
Index: 1100000
Index: 1200000
Index: 1300000
Index: 1400000
Index: 1500000
Index: 1600000
Index: 1700000
Index: 1800000
Index: 1900000
Index: 2000000
Index: 2100000
Index: 2200000
Index: 2300000
Index: 2400000
Index: 2500000
The public key is:  1 UsdbcaULhghdxvgsgK61TDvQiyN5h5CWgPcazi1MkMd
The secret key is:  Uint8Array(64) [
   81, 206,  64, 230, 210, 154,  23, 154,  20,  92,  99,
  218,  61, 213,  32,  51, 104, 188,  16,  59, 125, 158,
  105, 112,  73, 202, 218, 253,  23,  65,  72,  78,   7,
   35, 238,  51, 164, 145,  32, 147, 167, 120, 101, 224,
   22,  22, 122, 205, 185,  44, 123, 164, 109, 112,  52,
  119, 121,  73, 197, 203,  12, 191,  13,  56
]
Index: 2600000
Index: 2700000
Index: 2800000
Index: 2900000
Index: 3000000
Index: 3100000
The public key is:  uSd1r3ivnsHjjEKYYDrubSS2zogY72DfXNmVaJaPW7W
The secret key is:  Uint8Array(64) [
  218, 182,  23,  40,  64,  39,  77,  20,  78,  73,  23,
  147, 233,  36, 150, 149,  74, 141, 101, 255, 158,  85,
   19, 175,  76, 135,  75,  32,  47,  17,  66,  69,  13,
  111,  43, 248, 156, 247, 194,  11,   9, 227,  12, 223,
    7,  60, 135, 154, 190, 190, 252, 240,  40, 221, 103,
   21, 141,  79, 237,  91,  95, 236, 166, 237
]
Index: 3200000
Index: 3300000
Index: 3400000
The public key is:  2 USDzQkeQvio4pJeuYKwoa2PtMTGjNLbETrAJ7d5nEM2
The secret key is:  Uint8Array(64) [
   57,  72, 221, 246, 198,  60,  69, 211,  37, 236, 173,
  128,  88,  62, 162, 217,  15, 237, 237,   3, 144, 195,
    4, 120, 117, 241, 254,  39,  54, 114,   4,   2,   7,
    7,  51, 226,  50, 108,  93,  18, 175, 229,  87, 199,
  120, 144, 198,  40,  88, 114,  51,  91, 247, 113, 134,
  132, 244,  14, 194, 138, 244,  58,  18,  37
]
Index: 3500000
Index: 3600000
Index: 3700000
The public key is:  3 UsdFwE6YG44b7Zrr5wCb5GRgx8eZwPc6m8Yc4DqpPAE
The secret key is:  Uint8Array(64) [
   89, 236, 105,  44, 246, 148,  97,  28,  52, 152, 109,
   48, 189,  98, 242,  49, 126, 223, 143,  53, 153, 177,
   90,  82, 227,  36, 199, 255, 248,  36, 141, 164,   7,
   35, 236, 130,  42, 246, 184, 175, 166,  90,  30, 154,
  154,  87, 252,  72,  37, 253,  12,  49, 241, 164, 144,
  170,  48, 141, 105, 239, 236, 250,   6,  71
]
Index: 3800000
Index: 3900000
Index: 4000000
Index: 4100000
Index: 4200000
Index: 4300000
The public key is:  4 Usdz4EA5RgtYE7jQ7LyhW1qgrL4oHGwxjhk76z3VU1y
The secret key is:  Uint8Array(64) [
  158,  15, 245, 196,  27,  71, 222, 139, 178,  36, 161,
  192, 236,  41, 178,  20,  96, 192,  41, 242, 125, 124,
   48, 184,  45, 104, 196, 155,   2,   7, 107, 216,   7,
   35, 240,  33, 255, 109,  98, 190, 116, 157,   3, 222,
   62, 135,  68, 187, 181,  71,  11, 222, 101,  67, 121,
  169, 122,  43,  32,  50, 240, 104,  35, 100
]
Index: 4400000
Index: 4500000
Index: 4600000
Index: 4700000
Index: 4800000
Index: 4900000
Index: 5000000
Index: 5100000
Index: 5200000
Index: 5300000
Index: 5400000
Index: 5500000
Index: 5600000
Index: 5700000
Index: 5800000
Index: 5900000
Index: 6000000
Index: 6100000
Index: 6200000
Index: 6300000
The public key is:  5 UsdURuRpPH74VYAZReLW7JwZHn9ckAC7qatB7u9h6My
The secret key is:  Uint8Array(64) [
  106, 173, 239,  24, 246, 122, 160,  74,  68,  77, 145,
   90, 138,  98,  18, 107,  87,  42, 226, 231,  90, 203,
  138, 104, 255, 225,  41,  25, 196,  13, 159,   8,   7,
   35, 237, 149, 100, 227, 204,  52,  27, 103, 205, 130,
   44, 145, 231,  83, 205, 226, 162, 141,  87,  22, 195,
  129, 155,  93,  79, 158,  56, 253,  69,  52
]
Index: 6400000
The public key is:  USdsC65p1pP4VP1qMK2DcLCdq7BMBfsRjd3pb2Ea5kV
The secret key is:  Uint8Array(64) [
   65, 160, 213,  99, 114,  80, 242, 213,  59, 152, 224,
  132,  25,  95,  79, 136,  77, 216, 224, 122,  14, 152,
   51, 176, 209, 231,  48, 112, 143, 136, 151, 172,   7,
    7, 171,  10,   0, 134,  68, 104, 146,  43, 187, 225,
  250, 112, 213,  59, 222, 243,   3, 250, 167, 142, 189,
  242,  40, 115,  28, 203, 206, 219,  81,   2
]
Index: 6500000
Index: 6600000
Index: 6700000
Index: 6800000
Index: 6900000
Index: 7000000
Index: 7100000
Index: 7200000
Index: 7300000
Index: 7400000
Index: 7500000
Index: 7600000
Index: 7700000
Index: 7800000
Index: 7900000
Index: 8000000
Index: 8100000
Index: 8200000
Index: 8300000
Index: 8400000
Index: 8500000
The public key is:  usDuXCWbE3TSBThKZKe1kAYtsDNWuQNCxRmPT5UoEaF
The secret key is:  Uint8Array(64) [
   50,   7,  95, 157, 148, 108,  22,  63, 224,  61,  48,
   46, 179, 219,  14, 125, 145, 212,  55,  38, 229,  57,
  230,   8, 249,  14, 114,  64,   4,  55, 169,  33,  13,
  138, 253,  36, 225,  86, 230,  59, 249, 190, 161, 122,
    7, 104,  11, 128,  55, 152,  40, 232,  22, 131, 179,
  182, 161, 170, 211, 136,  91, 225, 134,  60
]
Index: 8600000
Index: 8700000
Index: 8800000
The public key is:  uSdEEHp8w15KJ3remqL9WiPkqt5RH74etZRvjCmt6rx
The secret key is:  Uint8Array(64) [
   61, 181,  89, 219, 251,  27,  20,  55, 233, 140, 243,
  234, 221,  83, 118,  76,   6, 215, 175,  45,  62,  66,
  201,  33, 190,  59, 187, 201, 254,  17, 174,   6,  13,
  111,  45,   9, 101,  56,  97, 132,  24, 127, 236,  71,
   92, 195, 124,  73,   4, 179,   5, 205,   7, 237,   0,
  176, 224,  54, 164,  32, 123,  52, 126, 157
]
Index: 8900000
Index: 9000000
Index: 9100000
Index: 9200000
Index: 9300000
The public key is:  USds2vtk3WhhA4wTqxCVZ4tE2dpYwiiGWX4zDvPztE9
The secret key is:  Uint8Array(64) [
  165,  87, 249, 225, 111,  74,   9, 137, 222, 180, 15,
   76, 116,  71, 164, 173, 162, 174, 119,  96, 222, 94,
    5,  20,  35,  91, 142,  33,  80,  41, 118,   6,  7,
    7, 171,   6, 134,  20,  65, 182,  82, 230,  66, 76,
  215, 242, 251,  31, 101, 188, 127, 197,  14, 165,  8,
  238, 165,   7, 199, 101, 247,  70,  90,  14
]
Index: 9400000
The public key is:  6 usdKVboFmAfVmieZ2z96JE55P8MNk954yDkEwD7V3m9
The secret key is:  Uint8Array(64) [
  202,  78, 141,  23, 123, 135, 220,  41, 183, 196, 238,
   17,  29,  85,  75,  52, 187, 172, 170, 216,  34, 187,
  116, 134, 128, 172,  28,  37,  10,   9, 220, 170,  13,
  139, 113, 254,  34, 172,  16,  10,   9, 248,  24, 242,
  221, 227, 173, 183, 120, 249, 139,  31, 217, 121,  77,
   54, 241,  66, 177, 221, 183,  27, 103, 136
]
Index: 9500000
Index: 9600000
The public key is:  7 USDdcLei1e8K9ZmzjgDJoicNQqTRbL6pM6PxUTauBDT
The secret key is:  Uint8Array(64) [
  136,  29,  21, 216,  96,  45,  42, 235, 138,  34, 184,
  199,  98, 158,  58, 240,  32,  18,  84, 140,  85, 224,
   43, 187, 114, 173, 111, 195, 129,  77,  28, 171,   7,
    7,  50,  24,   3,   7, 199, 168,  25, 202, 158, 142,
  107, 166, 217, 228, 169, 140, 142, 192,  77, 187, 228,
   67,  66, 107, 152,  80, 220, 117, 209, 234
]
Index: 9700000
The public key is:  uSD7KpmrFDSPVH3EbWLzE2cViQgqUQe1FcVPYg3P7kf
The secret key is:  Uint8Array(64) [
  208, 184,  68,  81, 171, 107,  97,  42, 142,  16, 194,
  166, 135, 251, 164,  79, 135,  34, 137,  20,  66, 166,
  212, 135,   0, 121, 164, 133,  24, 234, 255, 119,  13,
  110, 180, 170, 125, 221, 153, 226, 126,  23,  68, 229,
   72,  93, 193, 216,  85,  18,  27, 167,  60,  86,   2,
  180, 179,  56,  16,  79, 141, 111,  88, 108
]
Index: 9800000
Index: 9900000
Index: 10000000
Index: 10100000
The public key is:  uSDivM9EhfBseHBAKqENEj6ohL9Ugq5Sxc94rUuZm5L
The secret key is:  Uint8Array(64) [
  246,  30,  38,  84, 158,  44, 154,  78, 245, 116,   8,
  143, 161, 241, 202,  80,  16, 235,  98, 130, 127, 104,
   83,  51, 154,  31, 139, 101, 125,  88, 217,  66,  13,
  110, 183, 186, 148,  73, 170,   5,  26, 215, 138,  86,
    1,  88, 218, 255, 163, 107, 253, 230,  27,  35, 164,
  197, 199, 209, 136, 119, 128, 123,   3,  11
]
Index: 10200000
Index: 10300000
The public key is:  UsDqLC3FUZbE78F9Z8gBxNEZmNLqFuAFYt2nSKJR4BE
The secret key is:  Uint8Array(64) [
   74, 129, 251, 124,  87,  73, 114,  69, 223, 232, 113,
  208,  80, 138, 142, 159,  63, 255,  54,  99, 215, 194,
  132,  80, 123,  20, 115, 108,   2,  45,  80,  95,   7,
   35, 119, 154, 255, 214, 235,  10, 214, 192,  11, 133,
  142, 215,  85, 249, 234,  68, 246,  26,  86,  23,  30,
   56,   1, 209, 111, 248, 162, 229,  32, 141
]
Index: 10400000
Index: 10500000
Index: 10600000
Index: 10700000
Index: 10800000
Index: 10900000
The public key is:  usDcLJGRnswWbJNDjNuH2yyQPdFYQPB8hhiveuQdvp1
The secret key is:  Uint8Array(64) [
  202,  74, 211, 152,  64, 208,   0, 225, 106, 144, 234,
  208,   7, 246,  29, 250,  39,  94, 192, 235,  10,  31,
   75,  27,  49, 179,  39,  66,  81, 250, 237, 213,  13,
  138, 251, 170,  68,  40, 156, 171, 131, 176,  60,  83,
  244,  47, 204, 236,  68, 201, 142,  85, 104,  31, 220,
  235,  31, 170, 245, 128,  17, 183, 102, 106
]
Index: 11000000
Index: 11100000
Index: 11200000
Index: 11300000
Index: 11400000
Index: 11500000
Index: 11600000
Index: 11700000
The public key is:  uSDJXaBjzN6SrzagMTcS7UVErtEp66YnwRVimkHLEjF
The secret key is:  Uint8Array(64) [
  103, 182, 104,   8,   7,  80,  50, 214, 206, 192,  69,
   26, 146,  52,  65, 129, 118,  17, 228, 221, 252,   1,
  208, 157, 102,  17,  19, 193, 137,   0,  48,  51,  13,
  110, 181, 161,  66, 164, 101, 123, 179, 210, 168, 137,
  151, 176, 174, 170, 224, 115,  47,  10, 148, 154, 231,
  112, 180,  46,  65, 123, 252, 246, 117, 190
]
Index: 11800000
Index: 11900000
The public key is:  8 Usd8AdU57juwjgkEe6HiDPVHXFEKVNavHbz1bc8GwPT
The secret key is:  Uint8Array(64) [
   86, 152, 140, 222, 102, 222, 106,  64, 110, 115,   6,
  108, 102, 127, 155,  59, 159,  92,  22, 201, 151, 126,
  143,  27,  70, 201, 228, 181, 165, 198, 211, 198,   7,
   35, 235, 215,   8, 252,  99,  90,  19, 194,  96,  14,
  189,  44,  39, 241, 187, 168, 229, 159,  62,   9, 217,
  201, 114, 153,  51, 102,  46,   9,  92, 214
]
Index: 12000000
Index: 12100000
Index: 12200000
The public key is:  9 UsdWAWcMS5bd8jHvHNHDAe8SUZ6zYwxrB6wxqdKXBfV
The secret key is:  Uint8Array(64) [
   45,  89, 151, 245, 253, 157, 232,  18,  32, 226, 147,
  253, 170,  27,  73,  29, 215, 183, 238, 124, 172, 186,
  167,  83, 178, 209, 239,  77, 104, 109,  18,  99,   7,
   35, 237, 187, 154, 132,  50,   5,  79, 206,  65, 166,
   62, 161, 131, 116, 248, 204, 192, 192, 121, 115,  77,
   19, 190,  23, 236,   8,   5,  78,  55, 240
]
Index: 12300000
The public key is:  usDHJvxMKQx4KurdMYWwagJxW6pMVTutRm6t4RGPy84
The secret key is:  Uint8Array(64) [
    5, 132, 234, 192, 152, 180,  42, 249,  34, 140, 177,
  101,  37, 243, 140, 227,   7,  99, 187,  17, 218, 238,
  122, 190, 154,  83,   9,  83,  95,  99,  30, 102,  13,
  138, 250,   7,  55, 152,  25,  12, 219,   7, 245, 171,
   68, 219, 100,  36, 251, 135,  78, 153, 235, 226, 149,
  239,  69, 147, 146, 183,  54, 217, 235,  25
]
Index: 12400000
Index: 12500000
Index: 12600000
Index: 12700000
Index: 12800000
Index: 12900000
Index: 13000000
Index: 13100000
The public key is:  UsD8LePrfz5a6yr1P8CjJqt9p5ZGRuf8Vf8ci8DpEoA
The secret key is:  Uint8Array(64) [
   35,  18, 182,  33, 195,  94, 160,  22, 176, 241, 230,
  156,  40, 253,  66,  41, 197,  58,  96,  60, 134,  30,
  198,  98,  59,  33, 200, 120,  70,  49,  10,  35,   7,
   35, 116,  20,   7,  97, 149,  92,   8, 205,   5, 198,
  187, 233, 224, 185, 244, 223,  16, 253,  40, 117, 144,
   18, 253, 252,  31, 197, 200, 143, 145, 129
]

The public key is:  uSd7g64dzM6aywwqLxcpSBJ39ULQjuga4Trx1srcMAq
The secret key is:  Uint8Array(64) [
   63, 230,   4, 179,  47,  67, 241,  62, 148, 209, 189,
  125, 231,  25, 253,  25, 198, 109, 222,  78, 214,  59,
   74,  99, 157, 154, 226, 223, 224,  72,  37, 185,  13,
  111,  44, 120, 255, 115,  59, 130, 170, 249,  21, 206,
   87,  66, 233, 152, 251,  91, 125, 192,  23, 225,  84,
  240, 152,  61, 208, 117, 158,  92, 176,  82
]

The public key is:  10 USD18Tpj8hNARiiXieaWfNmHr5Kw36E5j7ACb415Fp9
The secret key is:  Uint8Array(64) [
    3, 201,  72, 198,   5, 224, 210,  48, 172,  56,  77,
  145, 156, 141,  79, 105, 230, 147,  46, 160,  41, 102,
   21, 207,  21, 192,  81, 205, 131, 165,  99,  70,   7,
    7,  46, 244, 107, 194, 230,  53,  53, 212, 209, 141,
   34, 207,  76, 152, 127, 206, 130,  87,  14, 215, 231,
  164,  34,  99, 254, 158,  15, 216,  49,  38
]

The public key is:  sWaPYLmK7QrMPy4EqSZ9PagX9NEAhHs8HzZ5aJraD8e
The secret key is:  Uint8Array(64) [
  132, 178, 173, 184,  86,  48,  75, 102,  74,  75, 249,
   43, 241, 236,  57,  40, 156, 179,  96,  57, 249, 115,
  141,  65, 152, 156, 136, 147, 164, 214, 138, 200,  12,
  240, 123,  85,   2,  96,  55,  59, 201, 236, 131, 114,
  151,  37,   0, 120,  23,   1,  95, 174,  56, 171, 226,
  204, 106, 148,  82, 160,  11, 206, 104, 131
]

The public key is:  sWApvzEwVhBjVJBc5gRDMtMRx1SUVCkMQmUCzTxgugm
The secret key is:  Uint8Array(64) [
  252,  45, 225, 155, 101, 111, 77, 151,  77, 240,  92,
  103,  62,  52,  55, 123,  10, 71,  27, 205, 162, 254,
  163, 152, 192, 248, 147,  58, 14,  97, 190, 241,  12,
  240,   5, 189, 127,  49, 233, 46,  17, 177, 131, 131,
  154, 186, 182,  98, 237,  58,  2,  31,  41,  21, 175,
  202, 111, 250, 109, 236,   3, 53,  39, 218
]
The public key is:  0 swapXGGphuhMFS8MSXTXSsHhadaE9TG9Ls4MS1wNZC2
The secret key is:  Uint8Array(64) [
  236,  91, 236,  79, 251, 122,   5, 236,  22, 123, 130,
   62,   1, 126, 194,  27,   4, 155, 186,  65, 223, 133,
  193, 146, 235, 245, 128,  80, 222, 169, 201,  59,  13,
   12, 193, 252,  21,  70, 233,  64,  20, 194,  73, 107,
   11, 114, 155, 215,  92, 254,  32,  46, 150,  62,  37,
  107, 216, 104,  71, 217, 255, 213, 142, 231
]

The public key is:  SWapHQjhzcAdAqAkJ93SJxJ2qCpZMRh9tge4aNhb144
The secret key is:  Uint8Array(64) [
  133,  59, 150, 101,  99,  39,  37,  32,  94,  67,  71,
   75, 133, 150, 103, 112, 175, 115, 123, 117,  92, 181,
  151, 218, 227,  21, 173, 211, 253, 166,  36, 220,   6,
  136, 248,  72, 114, 104,  46, 116,  11, 145, 195,  92,
   13, 116, 121, 118, 157,  79, 131, 219,  42,  28,   8,
   93,  49, 180, 203, 255,  43, 122, 223,  97
]



The public key is:  sWaPPooHExHeRbWiL1BtKHH8wLxUQ6mYePmsYQJnJyq
The secret key is:  Uint8Array(64) [
  134, 129,  51,  50,  17, 208, 160, 147,  56, 219,  38,
   28, 190, 102,  99,   2, 249, 242,  11,  25,  31,  61,
  234,  74, 247,  54, 215, 169, 249,  81,  62, 165,  12,
  240, 123,  81, 196, 167, 157, 195,  15, 111, 233, 233,
  104, 120, 197, 190,  75, 225, 204, 183, 170,  63, 252,
   34, 187,  40, 132,  10, 151, 133, 247, 124
]

The public key is:  swAP1pZTqjjuNExgUJd2FaQ2fDAMMm6adZXpp2KPcdD
The secret key is:  Uint8Array(64) [
  230,  11, 222, 138, 126,  54, 42, 119,  57, 30,   0, 65,
   30,   5, 171,  98,  67, 135, 64, 238,  74, 85, 145, 65,
   81, 145,  87, 147,  46, 133, 26,   0,  13, 12,  72,  3,
  100, 190,  29, 119,  67, 105, 52, 104,  75, 28,  39,  4,
  146, 150,  80,  29,  40, 116, 64, 199, 250, 66,  52, 67,
  150, 139,  45, 144
]



```


```
The public key is:  jusmJEEdhY5XZvP2aVNMzSyUp8W8JUdWY218UXjfYmV
The secret key is:  Uint8Array(64) [
    3, 161, 203, 242,  99, 173, 132,  79, 183,   4,   6,
  104,  32,  88, 116, 250, 229, 106, 209, 230, 159,  94,
  242,  12, 237, 205, 126, 126, 216, 250, 124, 180,  10,
  254,  46,  33, 186, 108, 195, 231,  31, 118,  37, 185,
  227, 176, 199, 116, 111, 204,  95, 102,  35, 114, 231,
  102,  59, 193, 195, 200, 170, 235, 225,   0
]
Index: 900000
The public key is:  JUStGMzkyWNML7QxHgBk7TWEUBq26UMZJdsCEDLemiR
The secret key is:  Uint8Array(64) [
   73,  39,  28,  22,  90, 185,  22, 140, 219,  56, 142,
   99, 254,  93, 190, 220, 210, 243,  12,  98,   7,  68,
  100, 231,  56,  93, 163, 208, 203,  49,  37, 139,   4,
  121, 232,  72, 105, 168,  63, 215,  64, 228,  42, 210,
  134, 202, 235,  36, 162, 246, 210,  36, 226, 105,  55,
  175,  47, 176, 243, 192, 147,   1, 113, 202
]
The public key is:  JUSYPqdXbNxjMJsj7hyzmcBYBqa44HuECFAi7NmP1ho
The secret key is:  Uint8Array(64) [
   91, 186,  14, 217, 180,  44,  95, 152, 121, 169,  93,
   69,  90,  79, 198,   3, 132, 129, 159, 128,  94, 113,
  244,  78,  86,  25, 204, 213,  42, 181, 149,  81,   4,
  121, 230, 146, 177, 208, 213, 189, 195,  29, 144, 185,
   48, 147,  86, 177,  11, 120,  19, 206, 175, 135,  29,
   53,  92, 154,  41, 162, 135,  58, 202, 142
]
The public key is:  jussk4D4VMzmSe7wg8FCLJQYpznhZMAy58oupzsRsLz
The secret key is:  Uint8Array(64) [
  137,  67, 168, 156, 102,  51, 171,   1, 194, 217, 140,
  148,  68,  64, 200,  31, 150,  24,  76,  25,   9, 102,
   13, 198,  65, 130,  42, 245,  30, 160,  25, 155,  10,
  254,  46, 175, 180,  84, 159, 129,  81,  82,  60, 170,
   21,  50, 120, 146, 136, 227,  54, 241, 156, 209,   3,
  137, 171,  71,  89, 235, 154, 201,  18, 207
]
The public key is:  JuSSpnJJpAkviFEiTW5xkftdshaes6Gm5buqPLj8u8v
The secret key is:  Uint8Array(64) [
   87, 102, 184, 238,  93,  18,  95,  77, 173, 166, 241,
   36, 128, 182, 124, 145, 131,  16,  81,  64, 112,  29,
   60, 102, 100, 217, 109,  37, 174, 221,  86,  26,   4,
  150,  42, 152, 201,  73, 142, 117, 239, 168, 250, 222,
   75,  38, 146,  74,  37,  23, 134,  10,  74,  86,  95,
  208, 193,  21, 134, 187, 101, 238, 141,  51
]
The public key is:  jUSZES7j6Sa397GzA3BsSUPGoWGYCeNy2X42BxWRQx3
The secret key is:  Uint8Array(64) [
  174, 178, 154,  73, 110, 157, 112, 182, 128,  71, 122,
  181,  82,  29,  97,  73,  83, 238, 133, 140, 240, 180,
  130, 205,  30, 113, 158,  20,  16, 230, 241, 250,  10,
  225, 107, 210, 189,  42, 132, 225,  21, 113, 215, 220,
  186, 237,  92, 131,  95,  88, 254, 167,  58, 214, 182,
    6, 138, 207,   2, 211,  54,  49,  58, 164
]
The public key is:  jUsodSugSjZSJ5zaWzq7jF1CcsrYphHCtSKdxWzRMUk
The secret key is:  Uint8Array(64) [
    4, 243, 203,  34,  99, 188,   8,  43, 106, 104, 135,
   61, 175,  51, 216, 250, 254, 253, 158, 180,  10, 182,
   34, 117, 134, 201, 104, 118, 125,   7,  72,  30,  10,
  225, 233, 212,  76,   7, 143,  89, 193,  49, 115,  75,
  174,  90, 235, 174, 237,  18,  35, 105, 149,  33,  56,
   89, 145, 238,  25, 192, 119, 232,  46,  73
]
The public key is:  jUSrhgfTJYU6ZbyF21MzH362o1YZZT73syS7eJtM8i5
The secret key is:  Uint8Array(64) [
   17, 105, 147,   6, 153,  40, 234, 117,  37, 152,  33,
  104, 200, 173, 189, 227,  19, 169,  81,  75, 160, 101,
  108, 255, 171, 246,  88,  33, 242, 187, 215,  50,  10,
  225, 109,  83, 144,   1,  77, 184, 123,   7,  91,  80,
    1, 125, 197,  73,  88, 164, 112,  62, 194,   7, 111,
  254, 144, 108,  65, 128, 190, 112, 225, 122
]
The public key is:  JUSziXppz7TF6PUiv79Ghx8NdvvaJcMnfKBp93ZW3G4
The secret key is:  Uint8Array(64) [
  245, 111, 102, 228, 137,  61,  38, 235, 247, 240, 202,
  143, 254, 248,  83,  24, 119,  45, 144, 142,  50,  83,
   26,   9, 239,  90, 159, 178, 146,   2, 238,  15,   4,
  121, 232, 214, 132, 217,   4, 212, 160,   3,  78,  48,
  195,  34,   3, 240, 142,  29,  47, 161, 118, 216, 255,
  243, 215, 227, 162,  33, 211, 204,  30, 249
]
Index: 5600000
The public key is:  JuSAPaNnxodT8m9saUwj988eQ7mGZymnF7ADZGwjcp1
The secret key is:  Uint8Array(64) [
  119, 162, 77,  21, 197, 241, 157, 237, 121, 228, 124,
   59, 238, 49, 129, 233,  29, 113,  81,  50, 215, 214,
  220, 180, 51, 151, 161,  43,  38,  67,   4, 238,   4,
  150,  41, 46, 196, 112,  41, 129,  53, 165, 113, 175,
  155, 184,  2, 251, 206, 228, 237,  10, 166, 223,  53,
  158,  63, 24, 120,  88, 150, 231,  17, 226
]
The public key is:  jusqZfRqWn328jHvbqahpzQPwsZgMia3EPt8UGZw9tb
The secret key is:  Uint8Array(64) [
    7, 153,  26, 210, 114,  44,  97, 247,  24, 109, 156,
   17,  30,  78, 104,  92,  25, 129,  21, 207,   1,  31,
  117, 204,  47,  95, 144, 238,  86, 246,  39,  55,  10,
  254,  46, 127, 179, 154, 183,  15, 108,  62, 228,  83,
  111, 203, 217, 180, 209,  61,  76, 132,  95, 171, 108,
   31, 241, 244,  53, 194,  28,  86,  20, 224
]
Index: 7300000
The public key is:  JusDYt2vLFwnzDhJg3nnqnyWjP82QMSarxUh4KAKLXH
The secret key is:  Uint8Array(64) [
  155, 233,   3, 150, 150, 176,  90, 223,  77, 102, 159,
    6,  44, 111, 134, 142, 156, 230, 224,  75,  22,  69,
  155, 179, 130,  87,  93,   0,  74, 222, 156, 141,   4,
  150, 166,  56, 207, 227, 146, 210,  36, 111,  24, 133,
  194, 112,  84,  55, 231, 254, 115,  53, 195, 192, 177,
  226, 231, 168, 197,  97, 190, 185, 149, 232
]
The public key is:  jUSj4Uas7U1cfTXatbRV2WMVbcYsFvVtmRLkYYspEMG
The secret key is:  Uint8Array(64) [
   32, 195, 210, 188,  44, 253,  13, 116, 203,  81, 229,
  177, 132,  51, 131,  43, 225,  32, 219,  41, 142, 171,
  199,  66,  24,  61, 202, 139, 187, 188, 125, 240,  10,
  225, 108, 171,  60, 105, 197,  37,  49, 101, 254, 153,
   28, 201,   6, 107, 144,  39, 235,  73, 224, 185, 137,
    4, 154, 153, 198,  49, 117,  97,  24, 131
]
Index: 8100000
The public key is:  JuSTeBQEBMqwEb7BRQBf9zKrjy6P6QhcnHa3vjvS7UN
The secret key is:  Uint8Array(64) [
   74,  35, 138,  33, 150,  69,  49,  37, 181, 103, 246,
  247, 143, 143, 234,  24,  17, 152, 236,  68,  47,   6,
  236, 154,  50, 212, 140,  98,  37,  14,  10, 145,   4,
  150,  42, 170, 201, 168, 225, 145, 236, 189, 148,  85,
  152, 161, 172, 221,  32,  29,  93, 185,  11,  11, 228,
  193, 138,  64, 213, 253, 138, 196, 112, 195
]
The public key is:  JusK7NENiC922Jg6f3MDvseudhpNmsGFAc81uBFPMpL
The secret key is:  Uint8Array(64) [
   19,  77, 175, 217,  20, 241, 177, 114, 209,  50, 236,
  239,  88, 196, 252, 162,  33,  52, 109,  83, 222, 207,
  252,  85, 252, 190, 155, 239,  47, 121,  37, 147,   4,
  150, 166, 179,  74,  23, 195, 253, 166, 231, 243,   4,
  166,  75, 212, 232,  91, 117, 156,  72,  39,  17, 157,
   73,  70,  71,  95, 172,  52, 241, 158,  25
]
The public key is:  juShyZc6E25KRMRUPAZKfr39yrGzhqPzvkNKt9hMLrG
The secret key is:  Uint8Array(64) [
   52,  84, 175, 242,  30,  82, 128, 225, 138, 226, 185,
   18, 207,  35, 145, 225, 207, 128, 159,   0,  75,  88,
  124, 254, 141, 153,  88,  28, 238,   6, 133, 246,  10,
  253, 177,  20,  32, 199,  79,   0, 164, 209, 108, 164,
  230, 215, 143,  83, 201, 167, 167, 124,  62, 114, 201,
  194,  30, 160, 109, 100, 159,  58,  82,  53
]
The public key is:  JusrsGFExu3tQGa2KLwxfH2ytmP3RwCrB78Kdj2Sbgp
The secret key is:  Uint8Array(64) [
  233, 127,  78, 178, 168,  36,  86, 228, 109,  80, 163,
  127,  23, 239,  76,  10,   6, 185,  97, 222, 231, 241,
  255,  35, 187,  63, 188, 142,  13, 123, 217, 234,   4,
  150, 169, 110, 211,  74,  21, 208,  72, 226,  61,  10,
  138, 129,  13, 232, 120, 162, 239, 137,  53, 195, 226,
  112,   0, 180,  21,   3,  88, 139, 208,   5
]
The public key is:  jUsvJdQZQP1E5S7yiN6tHZEo9ipH9AMrvc1Ykq8eDHv
The secret key is:  Uint8Array(64) [
  187, 220, 134, 183,  22,  89, 236, 187, 188, 108, 141,
  215, 175, 170, 121, 199, 187, 117,  64, 186, 202, 112,
  183, 215,  58,  93,  89,  66, 147, 167,  33, 230,  10,
  225, 234, 103,  88,  73,  76, 171, 223,  22,  64, 138,
   68, 120, 153, 180,   7,  67, 119, 186, 155, 214,  40,
  219,  39, 184, 135,  11, 106,  97, 206, 253
]
The public key is:  Jus9JkpWUX3U7PeyZNjibxV6efUg2Lp4MAAGTw6NWJ5
The secret key is:  Uint8Array(64) [
    5, 157, 174,  58,  27,  87,  78, 237, 245,  99, 187,
  217, 224, 153, 232,  84,   0, 152, 249, 148,  56,   4,
  165, 175,  81, 249,  87, 226, 170,  66, 188,  26,   4,
  150, 165, 219,  86,  19,  39,  58, 133,   7, 230, 104,
  213, 155, 207, 162, 150,  42,  94, 138,  16, 192, 197,
  220, 113, 187, 152, 226, 176, 194,  98,  74
]
The public key is:  jUSH7jRXjJisK5YbReNwrpY3XqW1DUvfLDDSP8kuiLj
The secret key is:  Uint8Array(64) [
  109, 176,  76,  29,  15, 130, 174,  84,  64, 199,  74,
  216,  85,  56,   0,  60, 179, 100, 220,  38, 216,  45,
   41, 228, 221, 158,  76,  32,  33, 103,  46, 227,  10,
  225, 106, 111, 191, 100, 106,  80, 197,  40,  38, 111,
  148,  41,  27, 151, 229, 128, 151,  43,  31, 216,  26,
  233,  63, 155, 103, 240,  27, 232, 248, 108
]
Index: 11000000
The public key is:  JuSye7Hro3FxNng3Lt59isZHkYRkXn22Y5ebM2eCqPN
The secret key is:  Uint8Array(64) [
   37,  98, 109,  31, 172, 161, 158,   1, 101, 168, 240,
   20, 255,  50, 187,  56,  27, 215,  94, 189, 157, 129,
    4,  90, 245,  96, 201,  25, 135, 239,  22, 215,   4,
  150,  45,  63, 152, 229,  87, 199,  22,  12,  16,  34,
   57, 171, 145, 191, 171, 102, 193, 197, 214, 111, 115,
   50, 179, 185, 179,  91, 159,  61, 119, 121
]
The public key is:  juSa8RJCTteb8xdDSrbEWhma73Kv6vRLHyUuQSkB74B
The secret key is:  Uint8Array(64) [
   78, 187, 111,  74,  57, 118,  52, 172, 175, 116, 152,
  106, 127, 184,  94,   7, 171, 179,  72,   3, 244,  78,
  241, 231, 207, 223, 187, 138,  53, 245, 245,  25,  10,
  253, 176, 103,  68, 202,  16,  39,  30, 159, 101, 197,
   31,   0,  69, 103,  68,  16,  54,  12,  30, 205, 218,
  250, 162, 226,  34, 116,  97,  76, 184,  48
]
The public key is:  jUSSkCiHANFnZZRPtqKU1S98Q4gLkbLMEk1pyt1TQbT
The secret key is:  Uint8Array(64) [
   22, 232, 244,  80, 210, 247,  55,  49, 158,  48, 142,
  211, 237, 168, 139,  65, 112, 251,   3, 123, 129, 134,
  229, 232,  63,  12, 106, 145, 224,  53, 209, 115,  10,
  225, 107,  67, 217, 135, 103,  32, 166, 114, 176, 155,
  254, 224,   2, 188,  47,  46,  78, 246,  69, 178,  41,
   83,  58,  77, 180, 103, 211, 111, 154, 122
]
The public key is:  JUsPNP4b4xA9m9FD1iSWXyU8sUCaMshuoQdvnq9u9Gm
The secret key is:  Uint8Array(64) [
   99, 108, 206, 215, 167,  11, 201, 240, 255, 163, 241,
  153, 106, 198, 239,  55, 110, 243,  75, 137,  97,  42,
   96, 220,  73, 223,   1, 109,  76,  80, 119, 120,   4,
  122,  98, 144,  81,  55,  48,  61,  16, 171, 124, 146,
   19, 147,  63, 157, 159, 183, 188,  18, 190, 144,  37,
   30, 138, 249,  18, 125,  24, 188,  43,  18
]
Index: 12200000
Index: 12300000
The public key is:  jusCrdQJ1RqmdVBMbb3C3XAehePLkuLkEe5kRbG5UgX
The secret key is:  Uint8Array(64) [
  152, 127,  81,  32, 234, 208, 114, 202,  50,  14, 230,
   28,  92, 249, 246,  56, 151, 138, 177,  63, 103, 170,
  153,  77, 209,  90, 137, 222,  78,  84, 240, 255,  10,
  254,  43,  87,  28, 248,  57,  26, 106, 144, 157, 173,
   94, 234, 202,  72,  13,  81,  10,  23,  64, 179, 221,
  108,  82,   9, 158, 236, 145,  86, 243,  16
]
The public key is:  JuSjWMVuGrfxzHzJ9VKjwQD84QoLN15ySEMAZ6n8PFQ
The secret key is:  Uint8Array(64) [
  227,  11,  90, 197,  61, 241, 238,  37, 108, 145,  60,
  143, 193,  92, 125, 156, 117, 211, 190,  40, 118,  45,
   97, 242,  81,  56, 113,  35,  60, 104, 125,  97,   4,
  150,  44,   8,  66, 249, 159,   5, 221, 173, 107, 251,
  197, 254,  53,  87, 118, 252,  44, 254, 227,  55, 223,
   98, 193, 229, 242, 187, 176, 216, 195, 227
]
The public key is:  jUSguftjJpkVTnKaQMEbgvEyRTpm6ve4ojz1RV5J8Q2
The secret key is:  Uint8Array(64) [
  100, 171, 111, 126, 184, 211,  48,  23,  74, 181,  42,
   15, 137, 206,   8, 143,  86, 200,  57, 185, 163,  73,
  110,   5, 146,  78,  38, 206, 247, 136,  76, 197,  10,
  225, 108, 123, 214,  14,  47,  49,  79,  18,  68, 242,
   48, 211, 172, 219, 114, 178,  32, 137, 121, 242, 228,
  177,  95, 106, 194, 138, 103, 133, 162, 155
]
Index: 13100000
The public key is:  juSxEuxfFg7Qr1M3UdZT8C2Fa6aixMPHdYb9rRk3msw
The secret key is:  Uint8Array(64) [
  217, 229, 191,  19, 119,  85, 191, 142, 103,  39, 163,
   71, 218,  80, 181, 112, 118, 213,  84, 252, 213, 130,
  217, 100,  48, 171, 221, 154, 116, 206,  71, 114,  10,
  253, 178,  78,  89,  56, 233,  69, 228, 118,  92,  69,
  225, 173,  93, 181,  99, 197,  58,  72,  20,  24, 150,
  190,   9,  28, 150, 184,  46, 203, 216, 250
]
Index: 13200000
The public key is:  JUS1UkGD9ans36VJQegSaPWQyrCAzMgJpfS5RsuPUtv
The secret key is:  Uint8Array(64) [
  128, 106, 193,  71, 133, 201,  22, 119, 131, 147, 76,
  169,  14, 216, 100, 209, 115,  44, 142,  76,  16, 17,
  131, 242, 172, 239, 206,  92,  14, 211,  41,   6,  4,
  121, 227, 233, 177, 176,   2,  72,  17, 170, 179,  6,
   84, 248,  97, 123, 207, 118, 230, 120,   5,  19,  3,
  102, 194, 162, 203, 236, 121, 217,  23, 127
]
Index: 13300000
Index: 13400000
Index: 13500000
Index: 13600000
Index: 13700000
Index: 13800000
Index: 13900000
Index: 14000000
Index: 14100000
Index: 14200000
Index: 14300000
Index: 14400000
The public key is:  JUscpSAf2UC8vfGaTAa3Exm5TvH1xmzerbWE5R68TPJ
The secret key is:  Uint8Array(64) [
   99, 140,  17, 188,  42, 243,  85, 219, 147, 252, 223,
  212, 161, 102, 129, 212,  46, 240, 225,  18, 152, 200,
  171, 186,  42, 199,   1,   9,  47, 248,   6, 233,   4,
  122,  99, 184, 147,  24, 205,  38, 190, 193, 247, 157,
  194,  61, 160,  92,  92, 126,  89, 175, 240, 213, 169,
   12, 162, 159, 105,  56,   5, 251,  72, 157
]
Index: 14500000
Index: 14600000
The public key is:  JusS76wiVXCf56h6H4UNprkwC172XQLSakZGDoTYwP3
The secret key is:  Uint8Array(64) [
  129, 123,   3, 186, 149, 240, 167,  20, 125,  14, 178,
  128,  11, 254, 182,  58, 145, 223, 146, 210, 138, 203,
  238,  37, 125, 147,  18, 121,  44, 251,  14, 116,   4,
  150, 167,  77,  98, 109, 223, 138, 103,  97,  52, 183,
   95,  22, 165,  10, 121,  58,  23, 129,   8, 218, 147,
  203,  39,  29,   8,  44, 216, 191,  78,  78
]
Index: 14700000
Index: 14800000
Index: 14900000
Index: 15000000
Index: 15100000
Index: 15200000
Index: 15300000
Index: 15400000
Index: 15500000
The public key is:  jusoYT5f6Cq2beWw3i9Z4XGLshU1CbUb1d1gSfZNAqc
The secret key is:  Uint8Array(64) [
   65,  64, 155, 129,  25, 188, 144, 241, 185, 147,  90,
  173, 177, 135, 246, 172, 226,   0,  27, 190,  40, 157,
   89,  32, 110, 223, 129, 124, 122, 208, 190,  85,  10,
  254,  46,  83,  47, 103,  91, 249, 243, 191,  31, 124,
  190, 209,  52, 226,  25,  94, 214,  80,   4,  63,  90,
  241, 219, 175,  95, 130,  91, 196, 124,  15
]
Index: 15600000
Index: 15700000
Index: 15800000
Index: 15900000
Index: 16000000
Index: 16100000
The public key is:  JUSzQ5uJfAf1B1fuYKKTFGbRYQeVBi6DWpJkguni6qk
The secret key is:  Uint8Array(64) [
  250,  43,  13,  31, 181,  84,  44,  98,  65, 173, 182,
  176, 217,  71, 253,  70, 200, 103, 201, 137,   0, 194,
  178, 213,  31,  13, 234,  44, 206, 161, 135, 207,   4,
  121, 232, 207, 131,  80, 207, 198, 252, 170, 142, 206,
  197, 208,   9,  92, 215, 140, 245, 159,  32, 115,  68,
   61,   8, 205,   1, 143, 228, 112,  31, 183
]
Index: 16200000
Index: 16300000
Index: 16400000
Index: 16500000
Index: 16600000
The public key is:  JuSLmS23KtyYWwk7Mggjprdiqxm4rGRdSFDoaXgmwBW
The secret key is:  Uint8Array(64) [
  211, 240,  45, 129,  70, 154,  97, 121,  37, 136,  14,
   23,   9,  24,  86,  60, 121,  72, 182, 168, 118,  75,
  155,  63, 158,  66,  64, 209,  43,  51, 252, 125,   4,
  150,  42,  19,  88, 201,  66,  39, 117, 133,  70, 214,
   93, 124,  45,  58,   0,  26, 127,  19, 115, 202, 243,
  182,  39,  95, 229,  58, 100, 178, 122,  73
]
Index: 16700000
Index: 16800000
Index: 16900000
The public key is:  jUsdDPqMXNYbBSFSqfqCP84vgH1VZofUygLtD1SmomA
The secret key is:  Uint8Array(64) [
  228, 187, 187, 196, 205, 177, 242,  41, 136, 184, 176,
  182, 173,  30,   0, 240, 195, 118, 221, 244, 114, 104,
  250,  12, 153, 149, 237,  66,  88, 210, 250, 168,  10,
  225, 232, 238, 226,  16, 108,  13,  65, 122,   0, 187,
  116, 166, 155, 185, 208, 101, 153,   0, 234, 114,  83,
  242,  81,  41,   9, 209, 222, 196, 207, 105
]
Index: 17000000
The public key is:  JUstfsw5Nbi7Fb4J5cDwynfLt1gv9g9xSuQ7WSwtWMR
The secret key is:  Uint8Array(64) [
  162, 119, 227,  74, 119, 117, 161, 244, 150, 227,
  126, 204, 232, 117,  37, 105, 197, 217,  29,  22,
  248,  56,  63, 102, 144,  83, 104, 245, 167, 218,
  184, 117,   4, 122, 101,  21, 197, 115,  76,  29,
  214, 112, 154,  26, 154, 248, 122, 172, 110, 124,
  146, 121, 206,  82,  67,   7, 222,  12, 201, 207,
  228, 159, 164, 236
]
Index: 17100000
Index: 17200000
The public key is:  juSB9MfRCqVYViRwo33zHukerYX1QrGWoVthUNfZxjD
The secret key is:  Uint8Array(64) [
  233, 218, 107, 100, 114, 154,  58,  34,  86,  86, 185,
   41, 192, 190,  13,  23, 245, 221,   7,  37, 217,  76,
   86, 215, 216,  52, 147, 237, 178,  92,  63, 221,  10,
  253, 174, 108, 251, 194, 204, 106, 225, 242,  38, 251,
  207, 169,  23, 246, 147, 238,  67, 247, 115, 195,  31,
  157,  21, 254, 223, 254, 196,  91, 159, 140
]
Index: 17300000
Index: 17400000
Index: 17500000
Index: 17600000
Index: 17700000
The public key is:  JusCnkvyCjhaYdd5bAafjyeaUicYbCk2R9ksAM6UeWs
The secret key is:  Uint8Array(64) [
   19, 209, 210, 205, 193,  92,  97, 208, 155, 191,  12,
  212,  45,  53,  57, 254, 232, 253, 148,  30, 127,  82,
   57,  37, 215, 240, 207,  48, 148, 120,  66, 111,   4,
  150, 166,  40,  14,   4,  47, 142, 129,  73,  77, 195,
   18, 193, 253,  59, 216, 239, 100, 212, 223, 109, 235,
    5, 242,  26,  86, 204, 119,  38, 121,  64
]
Index: 17800000
Index: 17900000
Index: 18000000
Index: 18100000
The public key is:  JUsRgDUmDbNAA6LQBJKJ89CtTZ8KLqMJxrPdLrtjktA
The secret key is:  Uint8Array(64) [
  253,  56, 250, 184, 254, 170, 171, 122, 249,  49, 234,
  207, 239,  59, 182, 234,  45, 130, 139, 170,  40, 223,
  164, 226, 220,  43,  40, 145,   5, 212,  28, 206,   4,
  122,  98, 195,  37, 128, 215, 170,  22,  80,  83, 250,
   99,  68, 164, 201, 203, 100, 207, 157, 186, 189, 108,
  240, 101,  41, 179, 133,   0, 140, 237, 195
]
The public key is:  JuSkHyKhKo5n9uiWkVTYqkaNZ2GPcaNtGs6SRLuppYa
The secret key is:  Uint8Array(64) [
   84, 200, 104, 202, 212,  75,  81,  24, 138, 189,  20,
   13, 105,  17,  34, 138, 191, 121, 221, 182,  69,  28,
   56, 154,  28,  94, 207, 166,  87,  28,  53,  14,   4,
  150,  44,  25, 150,  56, 114, 134,   9,  65, 152, 217,
  117,  85, 187, 241, 147,  44, 160,   6, 156, 215,  16,
  179,   4,  60,  55, 216, 242, 175, 249, 187
]
The public key is:  JusWND1L2YvoyrHhPHEyJrTqFnRK5AjHUPJetqw5pfc
The secret key is:  Uint8Array(64) [
    3, 117,  52, 224,  65, 248,  39, 241, 140, 246, 105,
  252, 196, 233,  73, 159, 250,  27, 231,  21, 223,  93,
  148, 178,  41,  57,  59,  10, 141,  91, 255, 121,   4,
  150, 167, 171,  59, 138,  10, 153, 154,  23,   4,  57,
  203, 242, 223,  24,  32,  41, 211,  47, 123, 191, 113,
  241,  66,   8,  88,  98, 208, 206, 102, 155
]
Index: 18200000
The public key is:  Jus2dRNxkjz35DHay79CCtgQbdaxXenFKpgnmNYuT7r
The secret key is:  Uint8Array(64) [
  180,  81,   9,  15,   5, 233, 234,  90, 254, 155, 248,
   42, 242,  87,  71,   3,  25,  90,  51,  10, 158, 255,
  242, 222, 191,  51, 166,  33,  46, 166, 237,  13,   4,
  150, 165,  72,  58, 211, 211,  85,  42,  19, 122, 133,
   54,  94, 228, 128, 170, 128, 207, 132, 134,  91,   4,
  194, 201, 185, 145, 203, 115,  67, 162, 229
]
Index: 18300000
The public key is:  JUswNsvQxsKSwXPwRrPGjY36Q3acb2ipfvqZALF82bd
The secret key is:  Uint8Array(64) [
  233, 199, 218, 218,  74,  82, 141, 102,  12, 226, 242,
  136, 217, 131, 186,  54,  18, 210, 115, 101,  53, 250,
   17,  43, 158, 154,  96, 158,  28,  31, 131, 143,   4,
  122, 101,  81, 101, 254,  62, 128,  85,  55, 100,  71,
   30, 198, 216, 173,  48,  18, 143,  72, 190, 236, 134,
  110, 147,  91, 136, 127, 104,  78,  88,  20
]
Index: 18400000
Index: 18500000
The public key is:  JUSLsydVE6BG6DERQkSGcEdhqGY2iw6ZH3rnydRxZXH
The secret key is:  Uint8Array(64) [
   20, 229, 214, 235, 243, 138, 187, 119, 132,  34, 43,
   81,  61,  63,  94,  13, 115,  97, 168,  27,  60, 49,
  152,  10, 104, 215, 114,  64,  19, 240,  42, 218,  4,
  121, 229, 149,  11, 234, 203, 253, 111,  15,  43, 95,
   60,  47, 243, 201,  16, 121,   4,  44,  88,  48, 22,
  172,  54, 104,  81,  24,  44, 155,  89, 116
]
Index: 18600000
The public key is:  JUsUByc1SoLHoR6wAAbFNTTHL7t217X7iYaWf1eXE8g
The secret key is:  Uint8Array(64) [
  151, 137, 231,  17, 114, 155,  77,  44,  22, 206, 125,
  127, 161,  52, 239,  51,  76,  85,  33,  34, 239,  88,
   54, 221,  86, 219,  17, 161, 142, 230, 205, 162,   4,
  122,  98, 250, 129,  80, 133,   7, 175,  77,  60,  92,
  157, 154, 167,  82, 228, 126,   0, 116,   2,  46, 178,
   48, 147,  99,  18, 173, 124, 116, 217, 145
]
Index: 18700000
Index: 18800000
Index: 18900000
The public key is:  JUsv8TCm2vSqHFaMuVXRHpXeFM82TCED6PapfaezdpJ
The secret key is:  Uint8Array(64) [
  153,  54, 206, 144, 108,  99, 243,  76,  46,  51, 141,
  212, 211, 239, 216,  77, 237,  18, 255,   9,  86, 208,
   80, 190, 102, 235, 178, 123,  18, 139,  14, 189,   4,
  122, 101,  53, 228,  63, 187, 127, 207,  50, 199, 207,
  164, 137,  39, 179,  98, 149, 142, 105, 210, 201, 255,
    8,   3, 225,  44, 243, 117, 170, 127, 159
]
The public key is:  jUsFhh6GNHGZNAqjcFnmiAQimkv1xYoixQXTkyXUbYj
The secret key is:  Uint8Array(64) [
   40,  76,  34, 161, 213, 194,  67, 126, 180, 198, 220,
   93, 220, 196,  90,   3,  95, 232, 121, 238, 247, 122,
  108, 197, 229, 152,  63, 239, 122,  79, 215, 224,  10,
  225, 231,  21,   4,  79,  52, 224, 150, 230,  79,  62,
  214,  59,  44,  59, 252, 142,   1, 202,  70, 115, 150,
   87,  47,  64, 248, 108, 198, 101,  96, 208
]
Index: 19000000
Index: 19100000
Index: 19200000
Index: 19300000
Index: 19400000
Index: 19500000
The public key is:  jUSgsgPozBvBd3oamAMXGVyA8ZfQq1zBQZjRZrpcFac
The secret key is:  Uint8Array(64) [
   77, 145,  68,  75,  94, 109, 140,  59, 224, 111,
  250, 240, 114, 255, 106, 185, 196, 239,  97, 180,
  223, 118, 104,   6, 210, 216,  42, 111, 198, 117,
  249, 218,  10, 225, 108, 123,  20, 113,  96, 162,
   88, 109, 123, 116, 254, 206, 223, 198, 187,  61,
   37,  46,  73, 253, 125,  39, 145, 113, 231, 212,
  238,  85, 198, 157
]
Index: 19600000
The public key is:  JuStKjHPhr8PKNKiZcfZjPvePAcdidh6acSe8J8T3K6
The secret key is:  Uint8Array(64) [
  187, 219,  53, 251,  89, 195,  57, 236,  65, 115,  24,
  251,  60, 172, 124, 223, 103, 217, 124,  71, 176, 246,
  224,  66, 193,  80, 172, 199, 215, 133, 245, 226,   4,
  150,  44, 202, 122,  61,  21,  23, 198, 223,  68, 245,
  113,  91,  65, 194,  28, 255,  58, 117,  22, 134,  89,
  130, 236, 204,  31, 108, 100,  79,  20, 193
]
Index: 19700000
Index: 19800000
The public key is:  juSztyH3oBXToaRkZ9ep43p9dvEmRBb7szMezXN6A6m
The secret key is:  Uint8Array(64) [
  154, 155,  66,  64, 216, 243, 178,  16,  23, 105, 222,
   29, 232,  52, 162, 140, 108, 187,  57,  45, 242, 149,
   92,  35, 175, 141,  50, 196,  47, 146, 185, 206,  10,
  253, 178, 136, 219, 170,  68, 187, 156, 242, 152,  43,
   19, 233,  59,  88,  50, 191,  52,  90,  65, 249, 146,
  253,  28, 231,  98, 196, 219, 125,  20,  42
]
Index: 19900000
Index: 20000000
The public key is:  JUSKeWJGgQHrTfJtm94LZDcCNuUawsp65xhVuWj3XAc
The secret key is:  Uint8Array(64) [
  120, 156, 215, 233,  82, 217, 209, 162, 125, 254, 155,
  174, 189, 175, 159,  22,  51,  39,   3, 178,  11, 138,
  178, 200,  84, 102, 156, 140, 213,  19, 209,  97,   4,
  121, 229, 121, 231,   4, 223, 113, 109,  46, 238, 159,
   97, 226,  26, 112, 205,  16,  84,  44,  53,  67, 178,
   50, 159, 219, 185,  65, 218, 209,  73, 117
]
Index: 20100000
The public key is:  JUsrostAAQMSpmGC3uTbReNTpRbvreWsGbtiYr52Ris
The secret key is:  Uint8Array(64) [
  131, 199,  85, 105, 106, 191, 137,  68,  21, 155, 165,
  172,  98, 245, 192, 247,  35, 214, 113, 136, 245, 110,
   16,  22, 175, 215,  96, 191,  89, 103, 131, 236,   4,
  122, 100, 236, 192, 231,  49,  97, 219, 225,   8, 107,
   37, 228,  98,   4, 189,  82,  47, 127, 253, 204, 191,
   11, 254,  70,  15,  28, 184,  86, 138,  36
]
Index: 20200000
Index: 20300000
The public key is:  jUSxndKoPANBQbiiyc5NSL7NDBXqfgVEykET5TbFyE1
The secret key is:  Uint8Array(64) [
  177, 154,  37,  39,  45, 246,  86, 159,  91, 241,  87,
  200,  63, 165,  93,  54, 241,  28,   4, 183,  42, 202,
  134,  96, 212,  57, 135,  99,  96,  29,  71, 206,  10,
  225, 109, 217, 155,  93, 161, 186,  75,  80,  64,  29,
    4, 169, 125,  45, 206, 112,  70,   5, 223,  37, 111,
  196, 218, 122,  10, 184, 181,  61,  28,  98
]
Index: 20400000
Index: 20500000
Index: 20600000
Index: 20700000
Index: 20800000
Index: 20900000
Index: 21000000
Index: 21100000
Index: 21200000
Index: 21300000
Index: 21400000
Index: 21500000
Index: 21600000
Index: 21700000
Index: 21800000
Index: 21900000
Index: 22000000
Index: 22100000
The public key is:  JUszUy6XRnv5E6cUUwoArudAM88Y6J6Bcc1vWUMEA9L
The secret key is:  Uint8Array(64) [
  158,  48,  26, 190, 177,  80,  70,  54,  56,  92, 124,
   46,  92,  33,  56, 131,  75,  13, 248,  60, 184,   7,
    8,  58, 167, 209, 227, 155, 170, 232,  70,  60,   4,
  122, 101, 149, 203, 112,  71,  17, 174, 188, 205, 140,
  253,  90,  65, 159, 173,   9, 162,  39, 215, 129, 124,
  202, 223,  94, 136,  83,  81, 173,  85,  15
]
Index: 22200000
Index: 22300000
Index: 22400000
Index: 22500000
Index: 22600000
Index: 22700000
Index: 22800000
Index: 22900000
Index: 23000000
The public key is:  JusiGKqBDmJh3Ry1nhZvNbLav7hJ5AQJFhsyNfjTeJ7
The secret key is:  Uint8Array(64) [
  226, 192,  80,  25, 170,  50, 110, 171, 135, 167, 116,
  215, 150, 203,  78, 115,  94,  30,   3, 116, 243,  49,
   80, 143, 245, 190,  24,  36, 168,  69,   4, 158,   4,
  150, 168, 177,  85,  69, 109, 178,  26, 221, 106, 152,
   70, 119, 225,  74, 113, 245, 200,  73, 204, 107,  30,
  167,  34,  67,  47,  10,  43, 115, 205, 196
]
Index: 23100000
The public key is:  juSF4FXKXXHFeZWBCGKjZAWF8L5zQfb66aD8hd4WfxM
The secret key is:  Uint8Array(64) [
    5, 192,   2,  88, 235, 177,  79,  12, 170, 245, 135,
  224,  42, 173, 178,  65,  48, 166,  16, 244,  27, 105,
  251, 207,  16, 248,  17,  69, 116, 213,  61,  22,  10,
  253, 174, 195,  39, 226, 241, 109, 255, 198,  73,   6,
  213,  10,  52,  21, 135, 233, 104,  87, 221, 250,  23,
  138,  81,  49, 206, 130, 165, 163, 237, 154
]
Index: 23200000
The public key is:  Jusczw4zDoMHKarvjmtpxQXVBuXhLhCZmtELS51tN4V
The secret key is:  Uint8Array(64) [
  110, 209,  84,  59, 161, 179,  86, 117, 206, 213, 193,
  159, 151, 204,  33, 253, 122, 126,  67, 228,   9, 112,
   88,   0, 181,  80, 172, 247, 216, 178, 101,  15,   4,
  150, 168,  61,  89,   7, 160, 112,   5, 103, 193, 127,
  179,  48, 136, 125, 195,   8, 209, 241, 158,  23, 135,
  124, 229,  58,   1,  66, 105, 119,  63, 246
]
Index: 23300000
Index: 23400000
Index: 23500000
The public key is:  JuSQYJjiD43BwK8jor8SCeM97H5kfEXssk3JhWT6oAE
The secret key is:  Uint8Array(64) [
   17,  99, 198,   2,   5,  87, 145, 204, 244, 155, 123,
  198,  68, 174, 113,  84,  69,  87,  70, 241,  24, 129,
    8, 138, 223, 229, 132, 137, 133, 200, 140, 188,   4,
  150,  42, 102, 121,  47, 120,  22,  70,  28, 220, 223,
  223, 252,  87, 100, 228, 141, 178, 185, 213,  68,  83,
   20, 139,  46, 219, 229, 151,  52, 204, 151
]
Index: 23600000
Index: 23700000
Index: 23800000
Index: 23900000
Index: 24000000
The public key is:  JUSffRem5GqSjibvLgdqye6sGo1ye5ryjwYpS8xzk7u
The secret key is:  Uint8Array(64) [
   22,  70, 104, 190, 146, 188, 233, 219,  79, 204, 154,
  121, 248,  51, 196, 107, 190, 203,  49, 255, 118,  77,
   16, 232,  15,  92, 174, 119,  85, 169,  48, 132,   4,
  121, 231,  50, 207,  52, 220,  89, 246,   0, 200,  84,
   82, 186,   7, 117,  19, 140, 235, 145, 107,  83,  15,
  169,  24, 204,  10, 131, 244,  69,  76,  20
]
Index: 24100000
Index: 24200000
Index: 24300000
Index: 24400000
Index: 24500000
Index: 24600000
Index: 24700000
Index: 24800000
Index: 24900000
Index: 25000000
Index: 25100000
Index: 25200000
Index: 25300000
Index: 25400000
Index: 25500000
The public key is:  JUS5tdJpgqioETUtqtc7QfpbnW4GvBRv7gFqHPqWhBm
The secret key is:  Uint8Array(64) [
   17, 130,  69,  91, 234, 193, 216,  60,  80,  23,  69,
   33, 197, 243,  70, 159, 252, 103,  74,  27,  75, 162,
  160, 169, 122,  75, 143, 106,  94, 243, 174, 168,   4,
  121, 228,  74, 224,   3, 221, 126, 174, 113, 205, 192,
  146,  55,  38, 112,  92, 141,  65,  81,  60,  31, 136,
  215, 127,  64, 172,   4, 154, 249, 213,  88
]
Index: 25600000
Index: 25700000
Index: 25800000
Index: 25900000
Index: 26000000
Index: 26100000
Index: 26200000
Index: 26300000
Index: 26400000
Index: 26500000
Index: 26600000
Index: 26700000
Index: 26800000
Index: 26900000
Index: 27000000
Index: 27100000
The public key is:  jusYwgbPqHqgqs9LV8fPJVZVf25SfgBzGDG9KAwfwNv
The secret key is:  Uint8Array(64) [
  165, 212,  21, 242, 210,  41, 219,  52,  33, 110,  26,
   14,  34, 209, 141, 233, 229, 250, 129, 160,  15, 153,
  203, 163, 222, 231, 179, 222, 170, 179,  61, 244,  10,
  254,  45,  17, 151,  51, 201, 202, 217,  19, 162,  10,
  149, 250,  60, 240,  91,  64, 202, 134,  86,  83, 148,
  225, 218,  55, 133, 220, 234,   0, 255, 255
]
Index: 27200000
Index: 27300000
Index: 27400000
Index: 27500000
Index: 27600000
Index: 27700000
Index: 27800000
Index: 27900000
The public key is:  JUSbYeo18ka5Han1LJnJb32PEutuevfQ8QtJV7mCcTa
The secret key is:  Uint8Array(64) [
   92, 221, 176,   9, 218,  94,  75,  51,  44,  84, 176,
   44, 237, 190,  83, 221, 175, 190,  35, 109,  37,  63,
   61, 179,  61, 195, 180, 245, 230, 130, 222, 103,   4,
  121, 230, 216,  32,  25, 233, 246,  61,  14,  52, 153,
   60, 188,  31, 132, 146, 213, 145, 196, 181,  78, 206,
  144,  91,  14, 203, 134, 132, 200, 240, 169
]
Index: 28000000
The public key is:  juSpkSboSAhjXXNVU8FJR8E6fWyfk8ciBG4LDkG66MU
The secret key is:  Uint8Array(64) [
  102,  91, 253, 198,  50, 171, 144, 155,  78,  25, 100,
  242, 180, 236, 144,  90, 150,   9, 240,  18, 183,  31,
  228, 149,  90, 234,   6, 107,  19, 153, 135, 230,  10,
  253, 177, 169,  87,  13, 207, 250,   8, 207,  16, 151,
  223, 147, 218, 112,  68,  40, 250, 215,  63,  21,  35,
  236,  52,  87, 218, 121,  58, 150, 234, 111
]
Index: 28100000
Index: 28200000
The public key is:  JusdgAEdqE8SVpqMapUatBbDJWWnDmSo3DMbLG4KcEe
The secret key is:  Uint8Array(64) [
  163,  97, 235, 169, 179, 248, 164, 124, 131, 207,  60,
   51, 155, 240, 158, 143, 167, 213,  64, 224, 200, 194,
  224,  90,  61, 171,  80,  12, 205,   0, 168, 153,   4,
  150, 168,  76,  62, 239,  69,  35,  69, 107, 190, 167,
  112, 228, 141, 192, 143,  87, 117, 212,  89,   1, 211,
  236, 146,  27, 157,   2, 251, 250,  97,  35
]
Index: 28300000
The public key is:  JUSg6YVVtCLRrDbbTyALkyVSCbFQX4zT2rTih49hz1T
The secret key is:  Uint8Array(64) [
   43,  31, 135, 223, 108, 233,  49,  38, 197,  46, 253,
   30, 108, 133, 240, 216, 185, 182,  15,  76, 142, 243,
  111,  34, 194, 192, 157,  57, 127, 111,  23, 107,   4,
  121, 231,  60,  89,  85, 244,  24,  95, 111,  55,  94,
  251,  20,  53, 135, 142,  16,  66, 194, 161, 149,  96,
  169,  37, 159, 134,  44, 242, 110,  45,  62
]
Index: 28400000
Index: 28500000
Index: 28600000
Index: 28700000
Index: 28800000
The public key is:  JuSKAUbruN7VhNdex5tFmqdqfLuH2xqYh6xW927iQLM
The secret key is:  Uint8Array(64) [
  120,  95,  84,  88,  69,   0, 226, 145, 137, 127,  41,
  180,  21,   3,  31, 254,  56, 190, 236,  74, 220, 100,
  174, 128,  74,  85,  15, 123,  97,   2, 159,  18,   4,
  150,  41, 240,  11,  13,  11,  17, 155, 120,  17,  25,
  157,  13,  18, 239, 182, 115,  73,  33,  10,  59, 199,
  225, 224,  58, 142,  64, 220, 150,  26, 134
]
Index: 28900000
Index: 29000000
The public key is:  jUS2EDCCi1PvFupywfApDU969ccTwyZkBiDBnKTcxsD
The secret key is:  Uint8Array(64) [
  128,  93, 169, 184, 182, 116, 234,  39,  17, 131,  99,
   19, 154,  55, 201,  24, 124, 155,  33,  61, 132, 207,
    8, 174,   4,   7,  63, 200, 141, 177,  27, 170,  10,
  225, 105,  39, 202,  61, 130,  59, 137,   3,  55,  59,
  108,  22, 158,  80, 161, 123, 185, 154,  54,  47,  72,
  219,  96,  41, 170, 212, 195, 141, 130, 180
]
Index: 29100000
Index: 29200000
Index: 29300000
Index: 29400000
Index: 29500000
The public key is:  JUS8UwzzcWNHSvHMNJKgD4zddRWWubi1bL4RsDy3Jjz
The secret key is:  Uint8Array(64) [
  252,  86,  87,  31,  72,  44, 134, 174, 226,  36, 237,
  244, 249,  10,  94, 194, 195, 153, 154, 188, 209, 207,
  103, 203, 203,  40, 228, 163,  93, 135,  97, 215,   4,
  121, 228, 131, 247,  83, 130, 109, 181,  13,  22, 123,
  186,  36,  46, 240, 254, 232, 179, 216, 188, 144,  41,
   31,  62, 206, 103, 173,  32, 234, 185, 241
]
Index: 29600000
Index: 29700000
Index: 29800000
Index: 29900000
Index: 30000000
Index: 30100000
Index: 30200000
Index: 30300000
The public key is:  JUSXjqAR8prZDxxwucN5h7XLYHTxx8teRJbzwe9bADd
The secret key is:  Uint8Array(64) [
   61, 141, 128,  67, 171,  64, 189, 177,  59, 243, 238,
  201,  71, 151, 106,  62, 103,  45,  98,   4, 240,  82,
  205,  56,  68,  75, 146, 120, 214,  30,  79,  23,   4,
  121, 230, 132,  66, 108, 194, 230, 155, 216, 203, 146,
  122, 108,  35,  29, 117, 201, 229,  62, 122,  12, 228,
  170,  54, 228,  65, 190, 222,  52,  87,  16
]
Index: 30400000
Index: 30500000
Index: 30600000
Index: 30700000
Index: 30800000
Index: 30900000
The public key is:  juSHBKLxBU6xcNKEx4bf31XS7y1WYGN72V12iZXT6SR
The secret key is:  Uint8Array(64) [
    4,  78, 212, 187, 247, 106, 226, 189,  97, 62,  93,
  181,   6, 137, 241, 153, 148, 208,  23,  79, 16,  52,
  136,  35, 245,   5,  91, 228, 229,  25,   8, 80,  10,
  253, 174, 241, 229,  39,  24,  49,  70, 253, 74, 186,
  123,  64, 249,  24, 245, 191, 143,  43,  70, 11, 203,
  227,  24,  91, 224, 170, 148, 160,  82,  38
]
Index: 31000000
Index: 31100000
Index: 31200000
Index: 31300000
Index: 31400000
Index: 31500000
Index: 31600000
Index: 31700000
The public key is:  juS7M1mUQJjaiK8GKSHUb8ZPBojsPbyurwpSXQqdXio
The secret key is:  Uint8Array(64) [
   70,  14,  67,  29,  10, 214,  23, 147, 213,  14, 94,
  193, 121,   8,  16, 179, 137, 193, 200, 208, 157, 44,
  255, 244, 118, 220, 156, 140,   4,  83, 119, 205, 10,
  253, 174,  25,  76, 147, 221,  22, 179,  95, 181, 12,
   32,  74,  63,   4,  37,  70, 244, 248, 198, 236, 89,
   94, 181,  41, 176,  22,  17, 247,  54, 176
]
Index: 31800000
Index: 31900000
Index: 32000000
The public key is:  juspRfMa3GwxuSydHMyyKnJSVnmsmLfCFSVZjP8i1Zk
The secret key is:  Uint8Array(64) [
   27,  27,  65, 102,  88, 234,  94,  37, 250, 166, 144,
   75,  58, 112, 191, 179,  83,  28, 113, 242,  95,   8,
   52,  32, 105,  89, 116,  46, 245, 253, 161, 221,  10,
  254,  46, 102, 162, 136,  12, 246,  42, 111,  65, 188,
  193, 181, 196, 119, 164, 224, 232, 228, 243,  80,  93,
   96,  27, 106, 250, 243, 160, 229, 123, 131
]
Index: 32100000
The public key is:  JUSupeTZiALSsfX4H2i6Atttoy3DH1QJh8iFdKgrRKR
The secret key is:  Uint8Array(64) [
  200,  17,  69,  78, 134, 180,   7,  81,  95,  63, 240,
   47,  68, 194,  22,  55, 226, 108,  41, 195, 143, 105,
  187, 184,  81,  51,  96,  41,  76, 182,  94,  63,   4,
  121, 232, 106, 179, 163, 141,  82, 254,  23, 154, 212,
   99, 179,  64,  76, 232,  61,  96, 232, 183,  42,  34,
  242,  97,  91, 198, 137,  77,  90, 206, 228
]
Index: 32200000
Index: 32300000
Index: 32400000
The public key is:  jus957iLFkDtjFkADVUY5UFmrsGxX2M7nSoso9MXkFu
The secret key is:  Uint8Array(64) [
   48,  90, 103,  70, 101, 162, 123,  37, 252, 225,  24,
  241,  71, 205, 219,   1,  68,   5,  49, 154,  47, 139,
  235, 189, 129,  83, 129, 201, 105,  63,  81, 250,  10,
  254,  43,   3, 190, 152, 144,  53, 245, 224, 135,  27,
   68,  48, 239, 101,  48,  43,  97, 221, 185, 152,  38,
   40, 107, 120, 213, 217,  91,  37,  99, 220
]
Index: 32500000
Index: 32600000
Index: 32700000
Index: 32800000
Index: 32900000
Index: 33000000
Index: 33100000
Index: 33200000
The public key is:  JUStckHs9f1ws9rXdi1QQfJWmCujrfBM9DoCt9pQ3aW
The secret key is:  Uint8Array(64) [
  216, 251, 100, 234,  92, 197, 183, 108, 210, 205,
  204, 231, 165, 128,  78,  87, 172,  87, 238, 144,
   19, 153, 137, 158, 214, 113, 194,  94, 191, 254,
  187, 209,   4, 121, 232,  80,  39, 143, 146, 228,
  212, 221, 250, 228, 121, 208, 251, 230, 141,  10,
  144, 196, 138,  66, 242, 153,  82, 206, 139, 192,
  217, 239, 134, 167
]
Index: 33300000
Index: 33400000
Index: 33500000
Index: 33600000
Index: 33700000
Index: 33800000
Index: 33900000
Index: 34000000
Index: 34100000
Index: 34200000
Index: 34300000
Index: 34400000
The public key is:  juSjGvUbfZyACYBSen1Geb3FtZdVaE3HX5dJ2KnNBfk
The secret key is:  Uint8Array(64) [
  114, 120, 250, 196, 205, 150, 134, 197,  63, 119, 119,
   12, 208,  35, 118, 221,  55, 197, 128,  76,  46,  11,
   14,  48, 170, 161, 222, 206, 211, 142, 221,  42,  10,
  253, 177,  48, 191, 192, 188,  89,  93, 247, 124,  36,
  107, 111,  79,  99, 173,  51, 134, 164,  84,  32, 165,
  139,   7,  59,  75,  16, 234,  60, 127,  71
]
Index: 34500000
The public key is:  JusSmEz7MEKJsbuTGcEgRJ9kLTyHkKUkubxcfj4tLDY
The secret key is:  Uint8Array(64) [
  135,  26, 209, 151, 160, 157, 189, 104,  37, 138, 180,
  141,  55, 191, 222,  35,  37, 127, 221,  83, 113, 185,
   95, 187, 128, 238,  90,  83,  87, 106, 219,  91,   4,
  150, 167,  91, 222, 132,  42, 207,  67,  38,  10,  53,
  123,  51, 232,  95, 199, 175,  54,   6, 107,  93, 245,
  171,  47, 145, 193, 217, 151,  45,  37, 235
]
Index: 34600000
The public key is:  juSypdzpdoRkS4V32M6JvGnaPxXFNrpZUr9TmkKPMnp
The secret key is:  Uint8Array(64) [
  243,  83,   6, 111,  65, 206, 203, 147, 169,  75,  39,
  110,   4,  10, 122, 184, 238, 209,  93, 224, 214,  49,
   63,  50,  96, 245, 184,  30,  11,  61, 233, 183,  10,
  253, 178, 113,  47,  77, 112, 220,  57, 219, 230, 180,
   36, 234, 242, 238, 236,  43,  22,  14,  59, 191, 163,
  249, 161, 212,  12, 146, 126, 222,  31, 161
]
Index: 34700000
The public key is:  jusNDr3JzESUL6q9KRFkZUYYsNXTdhewN9YR2zE8u6a
The secret key is:  Uint8Array(64) [
   90,  66, 209, 202, 225,  66, 241,  76, 211, 188, 121,
  188, 227, 198, 174, 190, 147, 190,  26, 173, 162, 197,
   14, 202, 189, 152, 233, 132, 222, 127, 253,  61,  10,
  254,  44,  37, 108,  38,  80,  18,   7,  60,  13, 201,
    4, 195,  18,   1, 146,  26, 226,   4,  16, 221, 167,
  163, 228,  27, 202,  13,  44,  49, 227,  91
]
The public key is:  JuSCxEiKHUeJc8rEYJECmznMTPc4qhW1F38UbGsKzfT
The secret key is:  Uint8Array(64) [
   18, 132, 171, 182, 141, 188,  24, 248, 147,   1, 246,
  123,  44, 117, 208,  20, 105,  87, 134,  88, 190, 122,
   97, 229, 168, 183,   3, 231,  14, 167, 186, 195,   4,
  150,  41, 103,  58,  57, 207, 238, 194,  19, 189, 176,
    4, 136, 216,  57,  83, 196, 248,  85, 251, 219, 176,
  177,  15, 133, 224, 214, 144, 128,  49,  10
]
Index: 34800000
Index: 34900000
The public key is:  JUsDwbQSD6aaiYf335Qdv7tyCRA64mWF34TmEBmnZzN
The secret key is:  Uint8Array(64) [
  225,  46, 109,  80, 176, 117,  29,  11,  94,  18, 177,
   96,  18, 136, 179,  30, 107,  52, 231, 161, 225,  43,
   53, 154, 105, 158, 223, 147, 102,  78, 226, 194,   4,
  122,  97, 192, 167,   1,  49,  23,  43,  14, 181,  43,
   30, 251, 178, 190,  33, 192, 227,  45,  90, 117, 133,
  250, 252,  26, 237, 104,   2,   0, 144, 199
]
Index: 35000000
Index: 35100000
Index: 35200000
Index: 35300000
Index: 35400000
Index: 35500000
The public key is:  JuShC9prJwvS7f1VpLU2vgUkV5MzP18JYKH9ozRneGX
The secret key is:  Uint8Array(64) [
    3, 238,  77, 179, 170,  77, 159,  15, 183, 158, 27,
   34,  31,  46, 124, 119, 239, 119,  94, 130, 181, 45,
  173, 183, 139, 100,  81, 197,   9, 149, 232,  83,  4,
  150,  43, 213,  75,  14,   2,  30, 198, 172, 191, 28,
   10, 146, 192, 130,  41, 217, 176, 128,  10, 180,  5,
  243,  87, 225, 204, 240,  81, 137, 216,  96
]
Index: 35600000
The public key is:  jUsEAJF54BrNt2PGunjno3HNBg8yejbaEEzxFssaNk4
The secret key is:  Uint8Array(64) [
   84, 107,  57, 117, 130, 158, 221, 106,  20,  96,  23,
   91,  75,  53, 156,  77, 139, 180,  70,  19,  20, 123,
  200,  21, 223,  97, 200,   1,  50, 103, 163, 152,  10,
  225, 230, 243,  16, 217, 104,  88,  63, 191,  78,  29,
  125,   9, 200, 135,  55, 189,  39, 164,  35, 225, 177,
  112,  51, 135, 245, 222, 210,  96, 131,  61
]
Index: 35700000
The public key is:  JUSUYzg5ucVwNQ85RoUw6y3f4SFeNmW7zFVabFgzUbd
The secret key is:  Uint8Array(64) [
  150,  71, 162,  82, 154, 164, 249,  40, 233, 102,  83,
  173, 144,  71, 196, 214, 216, 216,  56, 100, 174,  24,
   96, 218,  63, 202, 128,  98, 168,  58,  80,  67,   4,
  121, 230,  62,  15, 119,  13, 143, 194, 155, 250, 188,
   23, 157,  10, 242, 184, 219, 139, 247, 238,  81,  61,
  160, 175,  51, 175,  12,  10, 156,  68, 188
]
Index: 35800000
Index: 35900000
Index: 36000000
Index: 36100000
Index: 36200000
The public key is:  JUS9NuBD55FFdR8XLcbHB4YYJFJY5kLMC7DfndnUGa9
The secret key is:  Uint8Array(64) [
  187,  13, 171, 153, 167, 115, 112, 209, 162,  84, 133,
  201,  24, 166, 140,  39,  15, 115,  21,  25, 217,  76,
   82, 148, 135,  47,  38, 194, 116, 116,  71,   5,   4,
  121, 228, 151, 178,  94, 246,  48,  20, 154, 197,  27,
  128,   0,  23,  97,  57,  75, 238,  24, 131, 208, 209,
  238,  52,  60, 153, 127, 128, 254,  81, 102
]
The public key is:  JuSvtMci3XEitDTn48wXgFdnC1L36sz8LCfTUJQeMLu
The secret key is:  Uint8Array(64) [
    7, 179, 152, 214,  95,  85, 217, 206,   2,  79, 234,
   11,  83, 121, 239, 169,  91, 105, 200, 122, 240,  17,
   50, 165, 224, 203, 235, 118, 117,  31, 119, 237,   4,
  150,  45,   2, 236, 170, 237, 178, 126,  34, 247,   1,
  182, 218, 100,  55,  65, 106,   2, 178,  62, 239, 107,
   69, 101,  82, 211, 159, 118, 228,  32, 234
]
Index: 37300000
The public key is:  JUsHP3e3KTZLETpUbRP9LTX1bu5KSffoxAra5nK5rsx
The secret key is:  Uint8Array(64) [
  193,  27, 240, 227, 149, 124, 150, 203,  80,  52, 185,
  162,  87,  77, 135, 136,  35, 151,  52, 199,  81, 126,
   79,  53,  48,  52, 174,  57, 103,  81, 236,  45,   4,
  122,  98,  12, 103,  14, 181,  12, 143,  31, 132, 166,
   30,  84, 190, 100,  28,  16, 166, 199,  24, 174,   3,
  208, 179,  67,  26, 225,  69, 107, 138, 207
]
Index: 37400000
The public key is:  JuSfEbwYykvuPeTLDAwJnSBUiLZte7tx9ehAoTG62Ez
The secret key is:  Uint8Array(64) [
   35, 185, 164,  29,  22,  12, 109,  44, 137,  68, 122,
   58,   7, 190, 176,  98, 249,  29,  21,  21, 204,  76,
   42,  21,  93, 254,  66, 180, 193, 106,  99, 230,   4,
  150,  43, 170,  43,   2, 187, 204, 177, 210, 216, 114,
  198, 239, 203, 105,  79,   1,  14,  24,  76, 237,  20,
  249, 229, 209,  81, 243,  65, 229, 153,  71
]
Index: 37500000
The public key is:  JUSf3iyrkYy8g8rL4BPhmhNUdxoJE9t7Qcaq7begup6
The secret key is:  Uint8Array(64) [
   78, 138,  41,  95,  31, 127,  88, 251, 211,  51, 114,
   50, 181,  22, 255,  68, 214, 228, 166, 204, 117, 219,
  167,  21,  35,  64, 145,  50, 188, 245, 248, 123,   4,
  121, 231,  37,  64,  25, 255, 200,  83,  35,  57, 107,
   63, 189,  22,  17, 107,  19,  11,  10, 106, 137, 199,
  183, 195, 171,  49,   6, 111,  28, 221,  35
]
Index: 37600000
The public key is:  jUSw5hhin2TRvMkdAMyWyfLhgjRAXC9cPJkMtwNHk3V
The secret key is:  Uint8Array(64) [
  131, 224, 250, 184,  13, 223, 135, 225, 227, 108, 119,
  178, 134, 143,  24, 111, 234, 233,  54, 107,  30,   7,
   89,  58, 156, 137, 201,  34, 204,   3, 127, 136,  10,
  225, 109, 180,   9,  71, 186, 174, 217,  23, 157,  72,
  119,  87,  56,  87,  88,  27, 109, 236, 135, 117, 124,
  122, 246, 240, 177, 191,  47,  76,  95, 236
]
Index: 37700000
Index: 37800000
Index: 37900000
Index: 38000000
Index: 38100000
Index: 38200000
Index: 38300000
The public key is:  jUsAYpyqDerjH1UPhuNPMcssdNsFUTskxKSdELZXfvf
The secret key is:  Uint8Array(64) [
  134,  90,  85, 200,  31, 235, 252,  41, 171, 236, 158,
  249,  29,  79, 216, 183, 238,  88, 173, 130, 154, 188,
  174, 229, 181, 187, 157, 210, 207, 147,  32,  38,  10,
  225, 230, 163, 130, 206, 206, 183,   9, 117,  74, 240,
  163,  70, 168,   6, 220,   4, 242, 173, 128, 152, 185,
  108, 201, 145,  82,  98,  27, 183,  57,  80
]
Index: 38400000
Index: 38500000
Index: 38600000
The public key is:  jUsSz6eGJ8WL2CMwNyPzbC2r97s5JZq5xVRvuyKNWR9
The secret key is:  Uint8Array(64) [
   92, 238,  99,  41, 202,   1, 178, 185,  17, 149, 214,
  106,  31, 157,  72, 221, 120,  87,  88,  84,  25,  12,
  220, 173,  11, 124, 106, 103, 108,   0,  63, 156,  10,
  225, 232,  13, 141, 237,  40, 228,  65,  47,  70, 143,
   46,  30, 166, 126,  23, 181,  14, 140, 190,  50, 217,
   46, 175,  29, 157, 132, 221, 201, 139, 116
]
Index: 38700000
Index: 38800000
Index: 38900000
Index: 39000000
Index: 39100000
Index: 39200000
The public key is:  JUS4DZo4SFQXD8YSUmrU4hzdbpPXonZew2QneFTZjm1
The secret key is:  Uint8Array(64) [
  182, 175, 245, 237, 126, 243, 205, 103,  56, 206, 150,
  226,  37, 126, 122, 152, 204, 222, 118, 166, 217, 232,
   72, 150, 242, 163,  10,  34, 127,  86, 133, 186,   4,
  121, 228,  38,   3,  39, 145, 148,  45, 196, 207,  48,
  140,  20, 126,  89,  88,  35, 214, 229, 153,  92, 161,
  253, 222,  19, 211, 190, 253, 133, 106,   0
]
The public key is:  jUsjBNLKqqR7Ygpn3fpeNCVDEtEcWndJa9wsM19QweU
The secret key is:  Uint8Array(64) [
   62,  74, 187, 244,  43,  12,  40, 194,  86, 134, 108,
  178, 245, 155, 103,  90,  14, 134, 114, 253,  81, 108,
   90,  71,  72, 213, 216, 240, 177,  88, 240, 118,  10,
  225, 233, 114,  71, 235, 193,  88, 187,  96, 197, 164,
  211, 136, 138, 182, 181, 237, 175, 135, 244, 222, 250,
   46,  86, 186,  13,  97, 232,  59, 172,  45
]
Index: 40100000
The public key is:  JUsd3WRDdqiTbqiQMUNRxvNyrscyB4GdkJfRKdkUAWQ
The secret key is:  Uint8Array(64) [
  117, 190,  98,  40,  99, 136,  86, 147,  87, 249,  55,
  126,  87,  61, 113,  62, 193, 112, 116,  42,  53, 169,
   18, 113, 149,  19,  21, 221,  27, 157, 211, 173,   4,
  122,  99, 189, 138,  42, 235,  52,  56,   3, 175, 168,
  234, 175,  60, 188,  57, 239,  74, 112,  52,  23, 253,
  178, 127, 194, 203, 228, 180, 114, 163, 213
]
Index: 40200000
The public key is:  juSEgZzSaxsFe7XAvNxp12yTeEYoWZJvEFuFPidJcZj
The secret key is:  Uint8Array(64) [
   82, 233,  67,  11,   0, 168, 182,   5,  98,  84, 155,
   95, 193,  99, 242, 186, 139, 221,  94, 178, 255, 253,
  164,  87, 124, 241,  18,  81,  24, 185, 180, 131,  10,
  253, 174, 186, 235, 220, 101,  22, 178,  82,  35, 243,
  163, 134, 196, 218, 215, 190,  90, 216, 144, 206, 139,
  202,  17, 117,   9,  35, 152, 156,  69,  94
]


```