# Running a Wanchain Node

### Prerequisites

1. [Golang](https://golang.org/doc/install)

1. [Wanchain Client](install-client.md)

### Run Node

**Example 1 - testnet:**

`gwan --testnet --rpc --rpccorsdomain "127.0.0.1" --rpcaddr "127.0.0.1" --verbosity=0 console`

**Example 2 - mainnet:**

`gwan --rpc --rpccorsdomain "http://localhost:<YOUR DAPP PORT>" --verbosity=0 console`

**HTTP based JSON-RPC API options:**

 `--rpc` *Enable the HTTP-RPC server*

 `--rpcaddr` *HTTP-RPC server listening interface (default: "localhost")*
 `--rpcport` *HTTP-RPC server listening port (default: 8545)*
 `--rpcapi` *API's offered over the HTTP-RPC interface (default: "eth,net,web3")*
 `--rpccorsdomain` *Comma separated list of domains from which to accept cross origin requests (browser enforced)*
 `--ws` *Enable the WS-RPC server*
 `--wsaddr` *WS-RPC server listening interface (default: "localhost")*
 `--wsport` *WS-RPC server listening port (default: 8546)*
 `--wsapi` *API's offered over the WS-RPC interface (default: "eth,net,web3")*
 `--wsorigins` *Origins from which to accept websockets requests*
 `--ipcdisable` *Disable the IPC-RPC server*
 `--ipcapi` *API's offered over the IPC-RPC interface (default: "admin,debug,eth,miner,net,personal,shh,txpool,web3")*
 `--ipcpath` *Filename for IPC socket/pipe within the datadir (explicit paths escape it)*

** Interact with blockchain through a JavaScript console: **

A JavaScript console can be used to use a web3 protocol to interact with
the blockchain. Blockchain JavaScript console can be invoked by either
attaching to an existing RPC server or through a running node itself.

**Method 1:**

 `gwan attach http://rpc-ip:rpcport`

 **Method 2:**

 `gwan --testnet --rpc --rpccorsdomain 127.0.0.1 --verbosity=0 console`

The web3 commands are defined by Ethereum foundation. Wanchain extends web3 commands with its unique functions for privacy transactions.

**Interact with blockchain by a nodejs script:**

In order to connect to your blockchain via RPC, make sure your node is running and that you used --rpc flag when starting up your node. We are assuming you are using localhost to run your dapp so you also want to make sure you have the following included in your node startup command `--rpccorsdomain 127.0.0.1`

 Using nodjs script: You need to install web module
```
 var Web3 = require('web3');
 web3 = new Web3(new Web3.providers.HttpProvider('http://localhost:8545'));
 web3.eth.getCoinbase(function(err,resp){
 console.log('coinbase',resp)
 });
 ``

 If you run this on the client, you should see the address of the account