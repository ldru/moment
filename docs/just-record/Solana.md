---
sidebar_position: 1
---

**# Solana Memo**

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