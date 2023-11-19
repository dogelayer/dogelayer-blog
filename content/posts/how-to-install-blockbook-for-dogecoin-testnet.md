+++
title = 'How to Install Blockbook for Dogecoin Testnet'
date = 2023-11-19T20:10:35+08:00
+++

## What is Blockbook?
Blockbook is a back-end service for Trezor Suite, But we can use it as a dogecoin explorer and api service.   
Blockbook is OpenSource and actively maintained.  
The Github repo address is: https://github.com/trezor/blockbook  

## Install and Run
1. To install Blockbook, you will need to use Linux Debian version 11 (Bullseye) or later.  

2. Blockbook is a complex software that utilizes Docker for compilation, so you need to install Docker.   
   For instructions on how to install Docker, you can refer to the following URL:   
    https://docs.docker.com/install/linux/docker-ce/debian/.  

3. Then use git to obtain the source code:   
    git clone https://github.com/trezor/blockbook  

4. Go to blockbook directory and run:  
    make all-dogecoin_testnet  
    This will take a considerable amount of time.

5. Go to blockbook/build directory and run:  
    sudo apt install ./backend-dogecoin-testnet_*.deb

6. Fix The Bug!  
   While writing this document, I discovered a bug. In the file /opt/coins/nodes/dogecoin_testnet/dogecoin_testnet.conf, the line [test] needs to be removed. Otherwise, the rpcport will not take effect, causing Blockbook to be unable to connect to the backend. so the config file looks like this:  
    ```
    daemon=1
    server=1
    testnet=1
    nolisten=1
    rpcuser=rpc
    rpcpassword=rpcp

    txindex=1

    zmqpubhashtx=tcp://127.0.0.1:48338
    zmqpubhashblock=tcp://127.0.0.1:48338

    rpcworkqueue=1100
    maxmempool=2000
    dbcache=1000
    # generated from additional_params
    discover=0
    rpcthreads=16
    upnp=0
    whitelist=127.0.0.1

    rpcport=18038

    ```

7. Now you can start synchronizing with the network:  
    sudo systemctl start backend-dogecoin-testnet.service

8. check the status of Dogecoind synchronizing:  
    sudo tail -f /opt/coins/data/dogecoin_testnet/backend/testnet3/debug.log

9.  If the blockchain is fully synchronized, you can start installing your Blockbook.  
   Go to the directory blockbook/build and run:  
   sudo apt install ./blockbook-dogecoin-testnet_*.deb

10. Run Blockbook:  
    sudo systemctl start blockbook-dogecoin-testnet

11. Check the status of Blockbook synchronizing:  
    tail -f /opt/coins/blockbook/dogecoin_testnet/logs/blockbook.INFO

## How to access Blockbook service?

1. You can access the explorer using the url: 
     https://127.0.0.1:19138/

2. You can access the api using the url: 
     https://127.0.0.1:19138/api/v2/

## Important: 
Blockbook uses a self-signed certificate.   
It is necessary to go to the address in your browser, confirm the certificate, and then add the address to your wallet.  
If you use curl, you can add -k param, like this:  
curl -k https://127.0.0.1:19138/api/v2/