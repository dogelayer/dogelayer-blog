+++
title = 'More Development Resources for Dogecoin'
date = 2023-11-18T21:14:13+08:00
+++

1. python-dogecoin - Friendly dogecoin API binding for Python 3 

    https://github.com/bmwant/python-dogecoin

    This package allows performing commands such as listing the current balance and sending coins to the Satoshi (original) client from Python. The communication with the client happens over JSON-RPC.

2. pycoin - Python-based Bitcoin and alt-coin utility library. 

    https://github.com/richardkiss/pycoin

    The pycoin library implements many utilities useful when dealing with bitcoin and some bitcoin-like alt-coins. It has been tested with Python 2.7, 3.6 and 3.7.

3. blockbook - Trezor address/account balance backend 

    https://github.com/trezor/blockbook

    Blockbook is a back-end service for Trezor Suite. The main features of Blockbook are:

    -   index of addresses and address balances of the connected block chain
    -   fast index search
    -   simple blockchain explorer
    -   websocket, API and legacy Bitcore Insight compatible socket.io interfaces
    -   support of multiple coins (Bitcoin and Ethereum type) with easy extensibility to other coins
    -   scripts for easy creation of debian packages for backend and blockbook

4. coinbin - A Open Source Browser Based Bitcoin Wallet.

    https://github.com/OutCast3k/coinbin

    Coinb.in supports a number of key features such as: 

    - Offline Compressed & uncompressed Address creation.
    - Offline Multisignature Address creation.
    - "In browser" Key (re)generation. 
    - Send and receive payments.
    - Ability to decode transactions, redeem scripts and more offline.
    - Build custom transactions offline.
    - Sign transactions offline.
    - Signatures are deterministic as per RFC 6979 (https://tools.ietf.org/html/rfc6979#section-3.2)
    - Broadcast transactions.
    - nLockTime support.
    - Add custom data to transactions with the use of OP_RETURN.
    - Support current Dark Wallet Stealth Address structure (as of version Alpha 7) for outputs.
    - Brain wallet support.
    - Compatible with bitcoin-qt
    - An offical .onion address for tor users.
    - Offline qrcode creator and scanning tool.
    - HD (bip32) support.
    - Supports altcoins such as litecoin.
    - Replace by fee (RBF) Support.
    - Segwit Support.
    - Bech32 address support.
    - Fee calculator - https://coinb.in/#fees
    - Transaction rebuild support for RBF and double spending.

5. python-mnemonic - Mnemonic code for generating deterministic keys, BIP39 

    https://github.com/trezor/python-mnemonic

    This BIP describes the implementation of a mnemonic code or mnemonic sentence -- a group of easy to remember words -- for the generation of deterministic wallets.

    It consists of two parts: generating the mnenomic, and converting it into a binary seed. This seed can be later used to generate deterministic wallets using BIP-0032 or similar methods.

6. bitcoinbook - Mastering Bitcoin 2nd Edition - Programming the Open Blockchain 

    https://github.com/bitcoinbook/bitcoinbook

    Mastering Bitcoin is a book for developers, although the first two chapters cover bitcoin at a level that is also approachable to non-programmers. Anyone with a basic understanding of technology can read the first two chapters to get a great understanding of bitcoin.