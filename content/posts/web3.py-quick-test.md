+++
title = 'Web3.py Quick Test'
date = 2024-01-02T11:52:31+08:00
+++
Web3.py is a python interface for interacting with the Ethereum compatible blockchain.  
Dogelayer will build a Dogecoin L2 based on go-ethereum, so we need to know how to access it.  

## Install
We need 3.7.2 or higher version of Python and using pip to install Web3.py:  
```
pip install web3
```

## Quick Test Code
```
from web3 import Web3, Account
from web3.gas_strategies.rpc import rpc_gas_price_strategy
from eth_account.signers.local import LocalAccount
from eth_account.datastructures import (
    SignedMessage,
    SignedTransaction,
)
from web3.middleware import construct_sign_and_send_raw_middleware
import json
import sys


def load_account(address: str, password: str):
    with open(f"{address}.json", "r") as input_file:
        keystore = input_file.read()
        account: LocalAccount = Account.from_key(
            Account.decrypt(keystore, password=password)
        )
        return account


def save_account(account: LocalAccount, password: str):
    address = account.address
    keystore = Account.encrypt(account.key, password=password)
    with open(f"{address}.json", "w") as output_file:
        output_file.write(json.dumps(keystore))
    return True


w3: Web3 = Web3(Web3.HTTPProvider("https://dltest-rpc.dogelayer.org"))

test_password = "123qwe"

if len(sys.argv) == 1:
    print("use new_account to make a new account")
    print("use transfer <from> <to> <amount> to make a transaction")
    print("use balance <address> to get balance info")
    exit(1)

if sys.argv[1] == "balance":
    if len(sys.argv) != 3:
        print("use balance <address> to get balance info")
        exit(1)
    address = sys.argv[2]
    balance = w3.eth.get_balance(address)
    print(f'balance: {w3.from_wei(balance, "ether")} ethers')

if sys.argv[1] == "new_account":
    account: LocalAccount = Account.create()
    address = account.address
    print(address)
    save_account(account, password=test_password)

if sys.argv[1] == "transfer":
    if len(sys.argv) != 5:
        print("use transfer <from> <to> <amount> to make a transaction")
        exit(1)
    from_address = sys.argv[2]
    to_address = sys.argv[3]
    amount = sys.argv[4]

    from_account = load_account(from_address, password=test_password)
    balance = w3.eth.get_balance(from_account.address)
    print(f'balance of from account: {w3.from_wei(balance, "ether")}')

    if balance == 0:
        print("give some ether to address: ", from_account.address)
        exit(2)

    w3.eth.set_gas_price_strategy(rpc_gas_price_strategy)
    gas_price = w3.eth.generate_gas_price()
    print(f"gas price: {gas_price}")

    transaction = {
        "from": from_account.address,
        "to": to_address,
        "value": w3.to_wei(10, "ether"),
        "nonce": w3.eth.get_transaction_count(from_account.address),
        "gas": 200000,
        "gasPrice": gas_price,
        "chainId": 16888,
    }

    signed_tx: SignedTransaction = w3.eth.account.sign_transaction(
        transaction, from_account.key
    )
    print(signed_tx)

    tx_hash = w3.eth.send_raw_transaction(signed_tx.rawTransaction)
    print(tx_hash.hex())

    receipt = w3.eth.wait_for_transaction_receipt(tx_hash, 10)
    print(receipt)

    to_balance = w3.eth.get_balance(to_address)
    print(w3.from_wei(to_balance, "ether"))

```

## Reference
- https://web3py.readthedocs.io/en/latest/quickstart.html
- https://github.com/ethereum/web3.py