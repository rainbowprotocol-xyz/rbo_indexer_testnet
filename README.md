# 🌈 RBO Indexer Testnet

Welcome to the **RBO Indexer Testnet**! This is your gateway to participating in the decentralized future by contributing to the RBO network. By running this application, you can:

- 🛠️ Generate RBO Transaction Blocks on top of Bitcoin
- ✅ Submit Blockheaders and hashes for validation
- 💰 Help expand the network and earn rewards (after Mainnet launch)

---

## 📋 Table of Contents

- [🌈 RBO Indexer Testnet](#-rbo-indexer-testnet)
  - [📋 Table of Contents](#-table-of-contents)
  - [🛠️ Prerequisites](#️-prerequisites)
  - [📝 Instructions](#-instructions)
    - [1. Run Bitcoin Core on Docker](#1-run-bitcoin-core-on-docker)
    - [2. Connect Bitcoin Core and Run Indexer](#2-connect-bitcoin-core-and-run-indexer)
    - [3. Verify Your Setup](#3-verify-your-setup)
    - [4. Upgrade Indexer](#4-upgrade-indexer)
  - [📞 Support](#-support)

---

## 🛠️ Prerequisites

Before you begin, ensure your environment meets the following requirements:

- **Operating System:** Ubuntu 22.04 or later
- **Docker:** Installed and running
- **Bitcoin Core:** Set up with Testnet 4 enabled [🔗 GitHub Repo](https://github.com/rainbowprotocol-xyz/btc_testnet4)

---

## 📝 Instructions

### 1. Run Bitcoin Core on Docker

1. **Create a directory** for Bitcoin Core data and clone the repository:

   ```bash
   mkdir -p /root/project/run_btc_testnet4/data
   git clone https://github.com/rainbowprotocol-xyz/btc_testnet4
   cd btc_testnet4
   ```

2. **Edit the `docker-compose.yml` file** with your preferred text editor:

   - **Volumes Section:** Choose a local path on your host computer.
   - **Server Configuration:**
     - Replace the **server IP, username, and password** with your credentials.
     - Ensure the following parameters are present:
       - `-txindex`
       - `"-rpcallowip=0.0.0.0/0"`
       - `"-rpcbind=0.0.0.0:5000"`

   **Note:** If you are new to Docker or Bitcoin Core, it's recommended to use the **default settings** provided in the `docker-compose.yml` file. Adjustments are optional and only necessary if you have specific requirements.

3. **Start Bitcoin Core** by running:

   ```bash
   docker-compose up -d
   ```

4. **Access the Bitcoin Core container**:

   ```bash
   docker exec -it bitcoind /bin/bash
   ```

5. **Create a new wallet**:

   ```bash
   bitcoin-cli -testnet4 -rpcuser=yourusername -rpcpassword=yourpassword -rpcport=5000 createwallet yourwalletname
   ```

6. **Exit the container**:

   ```bash
   exit
   ```

### 2. Connect Bitcoin Core and Run Indexer

1. **Download and set up the indexer**:

   ```bash
   git clone https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet.git && cd rbo_indexer_testnet
   
   # Get Latest rbo_worker binary
   # For x86_64
   wget https://storage.googleapis.com/rbo/rbo_worker/rbo_worker-linux-amd64-0.0.2-20240914-4ec80a8.tar.gz && tar -xzvf rbo_worker-linux-amd64-0.0.2-20240914-4ec80a8.tar.gz
   cp rbo_worker-linux-amd64-0.0.2-20240914-4ec80a8/rbo_worker rbo_worker
   
   # For arm64
   wget https://storage.googleapis.com/rbo/rbo_worker/rbo_worker-linux-arm64-0.0.2-20240914-4ec80a8.tar.gz && tar -xzvf rbo_worker-linux-arm64-0.0.2-20240914-4ec80a8.tar.gz
   cp rbo_worker-linux-arm64-0.0.2-20240914-4ec80a8/rbo_worker rbo_worker 

   ```
    
2. **Start the indexer**:

   ```bash
   ./rbo_worker worker \
    --rpc {bitcoin_core_endpoint} \ # the bitcoind endpoint 
    --password {bitcoin_core_password} \ # the password in bitcoind rpc
    --username {bitcoin_core_username} \ # the username in bitcoind rpc
    --start_height 42000 \ #indexing height, you can custom it
    --indexer_port 5050 # the running port of indexer, default is 5050
   ```

   If you are using the `docker-compose.yml` in [https://github.com/rainbowprotocol-xyz/btc_testnet4](https://github.com/rainbowprotocol-xyz/btc_testnet4), you should probably run:

   ```bash
   ./rbo_worker worker --rpc http://127.0.0.1:5000 --password demo --username demo --start_height 42000 --indexer_port 5050
   # Using nohup to run if you want to run indexer backend
   nohup ./rbo_worker worker --rpc http://127.0.0.1:5000 --password demo --username demo --start_height 42000 --indexer_port 5050 > worker.log &
   ```
   To customize running port, you can pass `--indexer_port [PORT_NUMBER]`. Default port is `5050`.

   You should see logs similar to:

   ```bash
   Aug 31 00:00:00.032 INFO[] global_height is 0, v: 0.1.0, n: rbo_worker
   Aug 31 00:00:00.244 INFO[] Latest height is ...Some(42000), v: 0.1.0, n: rbo_worker
   ```

### 3. Verify Your Setup

1. **Locate and open your JSON file**
   * check local folder and locate the json file:
   `./identity/identity.json`, in thte json file, you will see data structure like this :
   ```json
   {
      "bitcoin_p2tr": "bc1pzzzzzzzzzzzzzzzzzzzzzzzzzz",
      "bitcoin_wif_key": "yyyyyyyyyyyyyyyyyyyyyyyy",
      "principal": "xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxx"
   }
   ```
     * `bitcoin_p2tr` is the Bitcoin Taproot address generated by the `bitcoin_wif_key` below.
     * `bitcoin_wif_key` is the **SAME** key generated by the `private_key.pem`, it is used to import to other wif supported wallets, eg `Unisat` or `Wizz`. 
     * `principal` is the principal ID your indexer to submit data to the Rainbow Protocol network. 

2. **Log in to the [Testnet Explorer](https://testnet.rainbowprotocol.xyz/explorer)**:

   - Input the Principal ID and review the details.

3. :bangbang: **IMPORTANT SECURITY NOTE, MUST READ**
     1. You should save these file to somewhere **SAFE** 
        * `./identity/private_key.pem` 
        * `./identity/identity.json` 
     2. Keep them in the `identity` folder when the indexer is running
  
### 4. Upgrade Indexer

```bash
# Find the running process pid and kill it
# Change 5050 to the port you customized
/bin/netstat -ntpl | grep 5050 | awk '{print $NF}' |  awk -F"/" '{print $1}' | xargs kill -9 
# Enter the directory where the original rbo_worker is located
# Replace with the new rbo_worker
   # For x86_64
   wget https://storage.googleapis.com/rbo/rbo_worker/rbo_worker-linux-amd64-0.0.2-20240914-4ec80a8.tar.gz && tar -xzvf rbo_worker-linux-amd64-0.0.2-20240914-4ec80a8.tar.gz
   cp rbo_worker-linux-amd64-0.0.2-20240914-4ec80a8/rbo_worker rbo_worker
   
   # For arm64
   wget https://storage.googleapis.com/rbo/rbo_worker/rbo_worker-linux-arm64-0.0.2-20240914-4ec80a8.tar.gz && tar -xzvf rbo_worker-linux-arm64-0.0.2-20240914-4ec80a8.tar.gz
   cp rbo_worker-linux-arm64-0.0.2-20240914-4ec80a8/rbo_worker rbo_worker
# Start the new one 
  nohup ./rbo_worker worker --rpc http://127.0.0.1:5000 --password demo --username demo --start_height 42000 --indexer_port 5050 > worker.log &
```
 
---

## 📞 Support

If you encounter any issues or have questions, feel free to reach out via our [community forum](https://t.me/rbo_protocol/1).

---

Thank you for contributing to the RBO Network! Your efforts are helping build a decentralized future. 🌐

