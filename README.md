#  🌈  RBO Indexer Testnet

Welcome to the **RBO Indexer Testnet**! This is your gateway to participating in the decentralized future by contributing to the RBO network. By running this application, you can:

- 🛠️ Generate RBO Transaction Blocks on top of Bitcoin
- ✅ Submit Blockheaders and hashes for validation
- 💰 Help expand the network and earn rewards (after Mainnet launch)

---

## 📋 Table of Contents

1. [Prerequisites](#prerequisites)
2. [Instructions](#instructions)
   - [Run Bitcoin Core on Docker](#1-run-bitcoin-core-on-docker)
   - [Connect Bitcoin Core and Run Indexer](#2-connect-bitcoin-core-and-run-indexer)
   - [Verify Your Setup](#3-verify-your-setup)
3. [Support](#support)

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

   > **Note for Beginners:** If you are new to Docker or Bitcoin Core, it's recommended to use the **default settings** provided in the `docker-compose.yml` file. Adjustments are optional and only necessary if you have specific requirements.

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
   wget https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet/releases/download/v0.0.1-alpha/rbo_worker
   chmod +x rbo_worker
   ```

2. **Start the indexer**:

   ```bash
   ./rbo_worker worker --rpc {bitcoin_core_endpoint} --password {bitcoin_core_password} --username {bitcoin_core_username} --start_height 42000
   ```

   You should see logs similar to:

   ```bash
   Aug 31 00:00:00.032 INFO[] global_height is 0, v: 0.1.0, n: rbo_worker
   Aug 31 00:00:00.244 INFO[] Latest height is ...Some(42000), v: 0.1.0, n: rbo_worker
   ```

### 3. Verify Your Setup

1. **Locate and open your JSON file**:

   - The file is typically located in: `./identity/principal.json`.
   - Copy the long string resembling this format: `xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxxxx-xxx`.

2. **Log in to the [Testnet Explorer](https://testnet.rainbowprotocol.xyz/explorer)**:

   - Input the Principal ID and review the details.

3. **Important Security Note:** Copy your `./identity/private_key.pem` to a secure location. It should remain in the `identity` folder while the indexer is running.

---

## 📞 Support

If you encounter any issues or have questions, feel free to reach out via our [community forum](https://t.me/rbo_protocol/1).

---

Thank you for contributing to the RBO Network! Your efforts are helping build a decentralized future. 🌐
```
