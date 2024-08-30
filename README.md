# RBO Indexer Testnet

An incentivized RBO Indexer for Testnet.
By running this application, you will be able to:

- Generate RBO Transaction Blocks on top of Bitcoin
- Submit Blockheader and hashes to validate
- Help expanding the network and get rewards (After Mainnet launch)

---

## Table of Contents

- [RBO Indexer Testnet](#rbo-indexer-testnet)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Instructions](#instructions)


---
## Prerequisites

Before running, ensure you have the following dependencies installed:

- Ubuntu 22.04 +
- [Bitcoin Core with Testnet 4 enabled](https://github.com/mocacinno/btc_testnet4)

---

## Instructions
0. **Rune the bitcoin core mentioned above**:
   1. Follow the instructions on [https://github.com/mocacinno/btc_testnet4](https://github.com/mocacinno/btc_testnet4)
   2. Make sure you have rpc **endpoint**, **username** and **password** created, which will be used in the following step.

1. **Download release binary**:
   [https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet/releases/download/v0.0.1-alpha/rbo_worker](https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet/releases/download/v0.0.1-alpha/rbo_worker)

2. **Connect Bitcoin Core and Run indexer**:
   ```bash
   ./rbo_worker worker --rpc {bitcoin_core_endpoint} --password {bitcoin_core_password} --username {bitcoin_core_username} --start_height 42000
   ```

3. **Lookup the folder and check your commits**
   * check local folder and locate the json file:
  ```json
  ...
  ```

   * login to [Testnet](https://testnet.rainbowprotocol.xyz/explorer), input the Principal ID and see the result