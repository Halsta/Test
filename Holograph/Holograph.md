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
