+++
title = 'How to Mine Dogecoin on Testnet'
date = 2023-11-21T15:32:45+08:00
+++
If you are a Dogecoin developer, you will need Dogecoin on testnet or DOGETEST.  
There are few Dogecoin testnet faucet online, but all of them have rate limits.  
So, I want to mine on Dogecoin Testnet.  

## Mine software
I did a lot of research and finally found cpuminer-opt:  

https://github.com/JayDDee/cpuminer-opt  

cpuminer-opt is a CPU mining software that supports multiple algorithms, including Dogecoin, and it is actively updated and maintained.  
If you are running Windows OS, you can download the binary software from it's release page:  

https://github.com/JayDDee/cpuminer-opt/releases  

If you are running Linux OS, you can download the source code and build it yourself:  

https://github.com/JayDDee/cpuminer-opt/blob/master/INSTALL_LINUX  

## Start Mining
You need a Dogecoin testnet node to start mining.  
I have a node running on localhost, so I start cpuminer-opt like this:  

./cpuminer -a scrypt -o http://127.0.0.1:44555 -u node-rpc-user -p node-rpc-password --coinbase-addr=your-testnet-dogecoin-address -B  -S  

The cpuminer will run in background and log the mining infomation to syslog.  
Here is how I check the log:  

sudo tail -f /var/log/syslog

## Check your balance!
The Net mining rate is not high at all, you should solve your first block in 10 minutes.  
You can check your balance on chain.so, Here is my balance:  

https://chain.so/address/DOGETEST/necwQ4XzgAo4ybSb7yweGSGVfhpqUyZamn

I mined 3 million in just one night. I was very shocked! 

