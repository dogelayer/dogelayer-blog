+++
title = 'How to Use Blockbook as Bitcoinlib Service Provider'
date = 2023-11-20T20:31:26+08:00
+++

## Config Bitcoinlib Provider
The config file of Bitcoinlib provider is located at ~/.bitcoinlib/providers.json.    
"~" should be your home dir, If you are using Windows OS, It will be something like C:/Users/user_name/.  
We are using Dogecoin testnet as an example.  
The content of providers.json should contain the config below:
```
    "blockbook.dogecoin_testnet": {
        "provider": "blockbook",
        "network": "dogecoin_testnet",
        "client_class": "BlockbookClient",
        "provider_coin_id": "",
        "url": "https://your-blockbook-address-or-domain/api/v2/",
        "api_key": "",
        "priority": 10,
        "denominator": 100000000,
        "network_overrides": null
    }
```

## A simple test
Use your favorite editor to create a .py code file:
```
from bitcoinlib.wallets import *
from bitcoinlib.networks import *
from bitcoinlib.keys import *

wallet_name = "DogeTestBlockbook"
network = "dogecoin_testnet"

mne = Mnemonic().generate()
print(mne)
w = wallet_create_or_open(wallet_name, network=network, keys=mne)

address = w.get_key().address
print(address)

w.utxos_update()

info = w.info()
print(info)

```
Run the code above, It should run without problem and print out a lot of infomation including address and balance.  
You can charge to the address and run the code again, It should update utxo infomation and give you the right balance.  
If you need testnet dogecoin, you can visit: https://shibe.technology/