# RBO Indexer Testnet

An incentivized RBO Indexer for Testnet. By running this application, you will be able to:

- Generate RBO Transaction Blocks on top of Bitcoin

- Submit Blockheaders and hashes for validation

- Help expand the network and earn rewards (after Mainnet launch)

---

## Table of Contents

- [RBO Indexer Testnet](#rbo-indexer-testnet)

- [Prerequisites](#prerequisites)

- [Instructions](#instructions)

---

## Prerequisites

Before you start, make sure you have the following:

- Ubuntu 22.04 or later

- Docker installed

- [Bitcoin Core with Testnet 4 enabled](https://github.com/mocacinno/btc_testnet4)

---

## Instructions

### 1. Run Bitcoin Core on Docker

1. Create a directory for Bitcoin Core data and clone the repository:

   ```bash

   mkdir -p /root/project/run_btc_testnet4/data

   git clone https://github.com/mocacinno/btc_testnet4

   cd btc_testnet4

   git switch bci_node

   ```

2. Edit the `docker-compose.yml` file with your preferred text editor:

   - In the `volumes` section, select a local path that exists on your host computer.

   - Replace the server IP, username, and password with your own.

3. Start Bitcoin Core:

   ```bash

   docker-compose up -d

   ```

4. Access the Bitcoin Core container:

   ```bash

   docker exec -it bitcoind /bin/bash

   ```

5. Create a new wallet:

   ```bash

   bitcoin-cli -testnet4 -rpcuser=yourusername -rpcpassword=yourpassword -rpcport=5000 createwallet yourwalletname

   ```

6. Exit the container:

   ```bash

   exit

   ```

### 2. Connect Bitcoin Core and Run Indexer

1. Download and set up the indexer:

   ```bash

   wget https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet/releases/download/v0.0.1-alpha/rbo_worker

   chmod +x rbo_worker

   ```

2. Start the indexer:

   ```bash

   ./rbo_worker worker --rpc {bitcoin_core_endpoint} --password {bitcoin_core_password} --username {bitcoin_core_username} --start_height 42000

   ```

   You should see logs like this:

   ```bash

   Aug 31 00:00:00.032 INFO[] global_height is 0, v: 0.1.0, n: rbo_worker

   Aug 31 00:00:00.244 INFO[] Latest height is ...Some(42000), v: 0.1.0, n: rbo_worker

   ```

### 3. Verify Your Setup

1. Locate and open your JSON file:

   - Check the local folder for the file: `./identity/principal.json`.

   - Copy the long string, which looks like: `xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxx`.

2. Log in to the [Testnet Explorer](https://testnet.rainbowprotocol.xyz/explorer):

   - Input the Principal ID and view the results.

3. **Important:** Copy your `./identity/private_key.pem` to a safe location. Keep it in the `identity` folder while the indexer is running.

