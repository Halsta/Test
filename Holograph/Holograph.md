## installation 
### Packages
```bash
sudo apt update && sudo apt upgrade -y
```
### Install git
```bash
sudo apt install git 
```

### Install Nodejs and npm
```bash
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash - && \
sudo apt-get install nodejs -y && \
echo -e "\nnodejs > $(node --version).\nnpm  >>> v$(npm --version).\n"
```

### holographxyz/cli
```bash
npm install -g @holographxyz/cli
```
### Help Command
```bash
holograph config --help
```
```bash
holograph config:user --help
```
### Prerequisites

To run commands you will have to at least have an RPC URL for one of the supported blockchains. You can get an RCP URL from different neworks on services like Alchemy and Chainstack.

The second requirement is wallet private key and a password. We never save your private key as plaintext and require the password, so we can send transactions to the blockchain.

### Run
```bash
holograph config
```
You should export your rpc or use defolt one
### Export private keys
Instruction:
https://support.metamask.io/hc/en-us/articles/360015289632-How-to-export-an-account-s-private-key

## Faucet 
Matic:
https://mumbaifaucet.com/
Avax:
https://www.allthatnode.com/faucet/avalanche.dsrv
Goerli:
https://goerlifaucet.com/

### Start client
```bash
holograph faucet
```
To get testnet HLG tokens, you must run the holograph faucet command. You are allowed to claim 100 HLG once every 24 hours per blockchain. If you want to operate on multiple blockchains, you will need to call this command on every network.

### Bonding Into a Pod
To become an operator, you must bond HLG into a pod. You are required to maintain uptime or risk having your HLG slashed

```bash
holograph operator:bond
```

