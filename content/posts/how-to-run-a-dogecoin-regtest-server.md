+++
title = 'How to run a Dogecoin regtest server'
date = 2023-10-31T21:43:38+08:00
+++

Dogecoin’s regression test mode (regtest mode) lets you instantly create a brand-new private block chain with the same basic rules as testnet-but one major difference: you choose when to create new blocks, so you have complete control over the environment. The following example will let you run a regtest server.

1. Download Dogecoin binary from Github.
   
    https://github.com/dogecoin/dogecoin/releases

2. Run dogecoind with regtest arguments

    dogecoind -regtest -server -txindex -rpcuser=your-rpc-username -rpcpassword=you-rpc-password -rpcport=22666 -datadir=choose-a-data-dir

3. Generate blocks and get reward

    dogecoin-cli -regtest -rpcuser=your-rpc-username -rpcpassword=you-rpc-password -rpcport=22666 generate 100

4. Check balance

    dogecoin-cli -regtest -rpcuser=your-rpc-username -rpcpassword=you-rpc-password -rpcport=22666 getbalance

5. Have fun with your regtest network!