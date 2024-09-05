# FAQ

1. **Strictly following the latest documentation can resolve most issues.**  
   - Deployment Guide: [https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet](https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet)  
   - Testnet 4 Full Node: [https://github.com/rainbowprotocol-xyz/btc_testnet4](https://github.com/rainbowprotocol-xyz/btc_testnet4)

2. **Error:**
   ```bash
   Warning: failed to fetch block 42000, retrying in 2s: JSON-RPC error: transport error: Couldn't connect to host: Connection reset by peer (os error 104)
   ```
   **Solution:** Follow the latest documentation to reconnect to Testnet 4.

3. **Node stuck while running:**
   ```bash
   '2024-09-02 08:53:06.351730558 UTC' at configure_log(), log_file_name is:'./logs/indexer_1725267186.lopg
   Sep 02 08:53:06.352 INFO[dapp/rbo_worker/src/updateer.rs:116:9] global_height is 0, v: 0.1.0, n: rbo_worker
   Sep 02 08:53:06.382 INFO[dapp/rbo_worker/src/updater.rs:123:9] Latest height is ...Some(42408), v: 0.1.0, n: rbo_worker
   Sep 02 08:53:06.382 INFO[dapp/rbo_worker/src/updater.rs:137:9] new height is ... Some(42511), v: 0.1.0, n: rbo_worker
   Sep 02 08:53:06.691 INFO[dapp/rbo_worker/src/updater.rs:150:9] spvslength 2, v: 0.1.0, n: rbo_worker
   Sep 02 08:53:06.692 INFO[dapp/rbo_worker/src/updater.rs:177:9] indexers length 0, v: 0.1.0, n: rbo_worker
   ```
   **Solution:** Follow the latest documentation and rerun the node.

4. **Error:**
   ```bash
   Traceback (most recent call last):
   file "/usr/bin/docker-compose" line 33, in <module>
   exit( load_entry_point ('docker-compose==1.29.2', 'console _scripts', 'docker-compose')())
   file "/usr/lib/python3/dist-packages/compose/cli/main.py", line 81, in main command func()
   file "/usr/lib/python3/dist-packages/compose/cli/main.py", line 200, in perform_command project = project_from_options ('.', options)
   file "/usr/lib/python3/dist-packages/compose/cli/command.py", line 60, in project_from_options return get_project(...)
   file "/usr/lib/python3/dist-packages/compose/cli/command.py", line 152, in get_project client = get_client(...)
   file "/us/lib/python3/dist-packages/compose/cli/docker_client.py", line 41, in get_client client docker client (...)
   file "/usr/lib/python3/dist-packages/compose/cli/docker_client.py", line 170, in docker_client client = APIClient(use_ssh_client=not use_paramiko_ssh, **kwargs,
   file "/usr/lib/python3/dist-packages/docker/api/client.py", line 197, in __init_self. version = self. retrieve server version()
   file "/usr/lib/python3/dist-packages/docker/api/client.py", line 221, in _retrieve_server_version raise DockerException(docker.errors.DockerException: error while fetching server API version: Not supported URL scheme http+docker
   ```
   **Solution:**  
   The `docker-compose` version needs to be upgraded to 20.x if using Ubuntu 24.04.  
   Uninstall the old `docker-compose` version:  
   ```bash
   sudo apt-get remove docker-compose
   ```  
   Install the latest Docker Compose (v2.x):  
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```  
   Verify the installation:  
   ```bash
   docker-compose --version
   ```

5. **Error:**
   ```bash
   Error: Rocket failed to bind network socket to given address/port.
   thread 'main' panicked at /home/ubuntu/.cargo/registry/src/index.crates.io-6f17d22bba15001f/rock 279:9: aborting due to socket bind error
   note: run with RUST_BACKTRACE=1 environment variable to display a backtrace
   ```
   **Solution:**  
   The port is occupied. Run the following command to see the process ID (pid):
   ```bash
   lsof -i:5050
   ```  
   Then, kill the process using:
   ```bash
   kill -9 {pid}
   ```

6. **Error:**
   ```bash
   thread 'main' panicked at dapp/rbo_worker/src/logger.rs:78:55: No LOGGER_FILE in .env file: NotPresent
   note: run with RUST_BACKTRACE=1 environment variable to display a backtrace
   ```
   **Solution:**  
   Please create a `.env` file and refer to the following link to configure the log file path:  
   [https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet/blob/main/.env](https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet/blob/main/.env)

7. **How to confirm the node is running successfully?**  
   If you see the following message, it indicates the node is running properly:  
   ```bash
   Sep 04 15:09:01.222 INFO[dapp/rbo_worker/src/main.rs:357:5] No new blocks, wait for next cron job, v: 0.1.0, n: rbo_worker
   Sep 04 15:09:21.267 INFO[dapp/rbo_worker/src/updater.rs:116:9] global_height is 42708, v: 0.1.0, n: rbo_worker
   Sep 04 15:09:21.279 INFO[dapp/rbo_worker/src/updater.rs:123:9] Latest height is ...Some (42708), v: 0.1.0, n: rbo_worker
   Sep 04 15:09:21.280 INFO[dapp/rbo_worker/src/main.rs:357:5] No new blocks, wait for next cron job, v: 0.1.0, n: rbo_worker
   ```

8. **How to add `private_key.pem` to wallet?**  
   Most wallets do not support `.pem` files. The `.pem` file is located in the `identify` folder.
