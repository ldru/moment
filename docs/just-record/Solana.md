---
sidebar_position: 1
---

# Solana Memo

+ WormHole Bridge

  |   Item             |   Importance           |  
  |:---------------------:|:-------------------:|
  | Project folder   |  E:\BlockchainWallet\Argon\wormhole\wormhole-sdk-ts\examples     |
  |  创建包裹的Token  | $ tsx src/createWrapped.ts       |
  |  Bridge Token    | $ tsx src/tokenBridge.ts       |
  |  测试Log         | E:\BlockchainWallet\Argon\wormhole\wormhole-sdk-ts\examples\log.txt      |


+ Links

  | Useful Link        |   Halving Date            |  
  |:---------------------:|:-------------------:|
  |  Solana Mainnet  |  https://explorer.solana.com/     |
  |  Solana Testnet | https://explorer.solana.com/?cluster=testnet       |
  |  Solana Devnet | https://explorer.solana.com/?cluster=devnet       |

+ How to run AREC Demo Dapp on Solana Dapp
  + E:\BlockchainWallet\Argon\solana22\arec-sol-demo
  + ()
  + yarn dev


+ How to setup Solana development environment

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

+  Good.txt
      
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