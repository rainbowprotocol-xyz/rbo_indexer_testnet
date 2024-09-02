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


1. **Run the bitcoin core mentioned above**:
   1. Follow the instructions on [https://github.com/rainbowprotocol-xyz/btc_testnet4](https://github.com/rainbowprotocol-xyz/btc_testnet4)
   2. Make sure you have rpc **endpoint**, **username** and **password** created, which will be used in the following step.

2. **Clone this repo and download release binary**
   ```bash
   git clone git@github.com:rainbowprotocol-xyz/rbo_indexer_testnet.git && cd rbo_indexer_testnet
   wget https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet/releases/download/v0.0.1-alpha/rbo_worker
   chmod +x rbo_worker
   ```

3. **Connect Bitcoin Core and Run indexer**:
   ```bash
   ./rbo_worker worker --rpc {bitcoin_core_endpoint} --password {bitcoin_core_password} --username {bitcoin_core_username} --start_height 42000
   ```

   If you are using the `docker-compose.yml` in [https://github.com/rainbowprotocol-xyz/btc_testnet4](https://github.com/rainbowprotocol-xyz/btc_testnet4)
   
   You should probrobably run bash like this:

   ```
   ./rbo_worker worker --rpc http://127.0.0.1:5000 --password demo --username demo --start_height 42000
   ```

   You should be able to see logs like this:

   ```bash
    Aug 31 00:00:00.032 INFO[] global_height is 0, v: 0.1.0, n: rbo_worker
    Aug 31 00:00:00.244 INFO[] Latest height is ...Some(42000), v: 0.1.0, n: rbo_worker
   ```

4. **Lookup the folder and check your commits**
   * check local folder and locate the json file:
   `./identity/principal.json`, open and copy the long string like :`xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxx`
   
   * login to [Testnet](https://testnet.rainbowprotocol.xyz/explorer), input the Principal ID and see the result

   * Also, you should copy your `./identity/private_key.pem` to somewhere safe, and keep it in the `identity` folder when the indexer is running 