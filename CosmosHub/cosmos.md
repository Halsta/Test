# GAIA
## Packages
```bash
sudo apt update && sudo apt upgrade -y
```
## Dependencies
```bash
sudo apt install curl build-essential git wget jq make gcc tmux chrony -y
```
## Go
```bash
ver="1.19.1" && \
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && \
rm "go$ver.linux-amd64.tar.gz" && \
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile && \
source $HOME/.bash_profile && \
go version
```
## Moniker, whrite something cool
```bash
NODENAME=Do_not_copypaste
```
## Make your custom ports. You can chose from 10 to 65
```bash
GAIA_PORT=51
```
## Save and import variables

```bash
echo "export NODENAME=$NODENAME" >> $HOME/.bash_profile
if [ ! $WALLET ]; then
	echo "export WALLET=wallet" >> $HOME/.bash_profile
fi
echo "export GAIA_CHAIN_ID=cosmoshub-4" >> $HOME/.bash_profile
echo "export GAIA_PORT=${GAIA_PORT}" >> $HOME/.bash_profile
source $HOME/.bash_profile
```
## Binaries

```bash
cd $HOME
wget https://github.com/cosmos/gaia/releases/download/v4.2.1/gaiad-v4.2.1-linux-amd64
mv gaiad-v4.2.1-linux-amd64 /usr/local/bin/gaiad
cd /usr/local/bin/
chmod +x gaiad
```
```bash
cd $HOME
wget https://github.com/cosmos/gaia/releases/download/v5.0.8/gaiad-v5.0.8-linux-amd64
mv gaiad-v5.0.8-linux-amd64 /usr/local/bin/gaiad
cd /usr/local/bin/
chmod +x gaiad
```

```bash
cd $HOME
wget https://github.com/cosmos/gaia/releases/download/v6.0.4/gaiad-v6.0.4-linux-amd64
mv gaiad-v6.0.4-linux-amd64 /usr/local/bin/gaiad
cd /usr/local/bin/
chmod +x gaiad
```

```bash
cd $HOME
wget https://github.com/cosmos/gaia/releases/download/v9.0.2/gaiad-v9.0.2-linux-amd64
mv gaiad-v9.0.2-linux-amd64 /usr/local/bin/gaiad
cd /usr/local/bin/
chmod +x gaiad
```
```bash
cd $HOME
wget https://github.com/cosmos/gaia/releases/download/v10.0.2/gaiad-v10.0.2-linux-amd64
mv gaiad-v10.0.2-linux-amd64 /usr/local/bin/gaiad
cd /usr/local/bin/
chmod +x gaiad
```
```bash
cd $HOME
wget https://github.com/cosmos/gaia/releases/download/v11.0.0/gaiad-v11.0.0-linux-amd64
mv gaiad-v11.0.0-linux-amd64 /usr/local/bin/gaiad
cd /usr/local/bin/
chmod +x gaiad
```
```bash
cd $HOME
wget https://github.com/cosmos/gaia/releases/download/v12.0.0-rc0/gaiad-v12.0.0-rc0-linux-amd64
mv gaiad-v12.0.0-rc0-linux-amd64 /usr/local/bin/gaiad
cd /usr/local/bin/
chmod +x gaiad
```

```bash
cd $HOME
wget https://github.com/cosmos/gaia/releases/download/v13.0.0/gaiad-v13.0.0-linux-amd64 && \
mv gaiad-v13.0.0-linux-amd64 /usr/local/bin/gaiad && \
cd /usr/local/bin/ && \
chmod +x gaiad
```

## Config app

```bash
gaiad config chain-id $GAIA_CHAIN_ID
gaiad config node tcp://localhost:${GAIA_PORT}657
```
## For your own risk 
```bash
gaiad config keyring-backend file
```
## Init app

```bash
gaiad init $NODENAME --chain-id $GAIA_CHAIN_ID
```
## Seeds and peers

```bash
SEEDS=""
PEERS="https://state-sync-01.theta-testnet.polypore.xyz,https://state-sync-02.theta-testnet.polypore.xyz"; \
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.gaia/config/config.toml
```
## Genesis

```bash
cd $HOME
wget -O genesis.json https://snapshots.polkachu.com/genesis/cosmos/genesis.json --inet4-only
mv genesis.json ~/.gaia/config
```

## AddrBook
```bash
wget -O addrbook.json https://snapshots.polkachu.com/addrbook/cosmos/addrbook.json --inet4-only
mv addrbook.json ~/.gaia/config
```

## Custom ports 

```bash
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:${GAIA_PORT}658\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:${GAIA_PORT}657\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:${GAIA_PORT}060\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:${GAIA_PORT}656\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":${GAIA_PORT}660\"%" $HOME/.gaia/config/config.toml
sed -i.bak -e "s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:${GAIA_PORT}317\"%; s%^address = \":8080\"%address = \":${GAIA_PORT}080\"%; s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:${GAIA_PORT}090\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:${GAIA_PORT}091\"%" $HOME/.gaia/config/app.toml
```
## Pruning

```bash
pruning="custom"
pruning_keep_recent="100"
pruning_keep_every="0"
pruning_interval="10"
sed -i -e "s/^pruning *=.*/pruning = \"$pruning\"/" $HOME/.gaia/config/app.toml
sed -i -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"$pruning_keep_recent\"/" $HOME/.gaia/config/app.toml
sed -i -e "s/^pruning-keep-every *=.*/pruning-keep-every = \"$pruning_keep_every\"/" $HOME/.gaia/config/app.toml
sed -i -e "s/^pruning-interval *=.*/pruning-interval = \"$pruning_interval\"/" $HOME/.gaia/config/app.toml
```
## Minimum gas price

```bash
sed -E -i 's/minimum-gas-prices = \".*\"/minimum-gas-prices = \"0.00uatom\"/' $HOME/.gaia/config/app.toml
```

## Prometheus

```bash
sed -i -e "s/prometheus = false/prometheus = true/" $HOME/.gaia/config/config.toml
```
## Reset chain data

old

```bash
gaiad unsafe-reset-all --home $HOME/.gaia 
```
new

```bash
gaiad tendermint unsafe-reset-all --home $HOME/.gaia --keep-addr-book
```
# Service

```bash
sudo tee /etc/systemd/system/gaiad.service > /dev/null <<EOF
[Unit]
Description=Stake to Kolot
After=network-online.target

[Service]
User=$USER
ExecStart=$(which gaiad) start --home $HOME/.gaia --x-crisis-skip-assert-invariants
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
# Snapshot

```bash
wget -O cosmos_16549844.tar.lz4 https://snapshots.polkachu.com/snapshots/cosmos/cosmos_16549844.tar.lz4 --inet4-only

```
```bash
lz4 -c -d cosmos_16549844.tar.lz4  | tar -x -C $HOME/.gaia
```

## Register and start service

```bash
sudo systemctl daemon-reload
sudo systemctl enable gaiad
sudo systemctl restart gaiad && sudo journalctl -u gaiad -f -o cat
```
## synchronization status
```bash
gaiad status 2>&1 | jq .SyncInfo
```
# Validator stuff, in process
## Create-restore wallet

```bash
gaiad keys add $WALLET
```
```bash
gaiad keys add $WALLET --recover
```
```bash
gaiad keys list
```
## Load variables into the system
```bash
GAIA_WALLET_ADDRESS=$(gaiad keys show $WALLET -a)
```
```bash
echo 'export GAIA_WALLET_ADDRESS='${GAIA_WALLET_ADDRESS} >> $HOME/.bash_profile
```
```bash
GAIA_VALOPER_ADDRESS=$(gaiad keys show $WALLET --bech val -a)
```
```bash
echo 'export GAIA_VALOPER_ADDRESS='${GAIA_VALOPER_ADDRESS} >> $HOME/.bash_profile
source $HOME/.bash_profile
```
## Check balance
```bash
gaiad query bank balances $GAIA_WALLET_ADDRESS
```
## Register Validator
```bash
gaiad tx staking create-validator \
  --amount 1000000uatom \
  --from $WALLET \
  --commission-max-change-rate "0.1" \
  --commission-max-rate "0.3" \
  --commission-rate "0.08" \
  --min-self-delegation "1" \
  --pubkey  $(gaiad tendermint show-validator) \
  --moniker $NODENAME \
  --chain-id $GAIA_CHAIN_ID --fees 250uatom
  ```
  ## Edit validator
  ```bash
  gaiad tx staking edit-validator \
  --moniker=$NODENAME \
  --identity=<your_keybase_id> \
  --website="<your_website>" \
  --details="<your_validator_description>" \
  --chain-id=$GAIA_CHAIN_ID \
  --from=$WALLET --fees 250uatom
  ```
  ## Domain
 ```bash
 gaiad tx domain register do-not-copypast --data="$BasicData" --from=$WALLET --chain-id=$GAIA_CHAIN_ID --gas 2100000 --fees 2100uatom --output json -b block
 ```
  
  ## Peer list
   ```bash
  curl -sS http://localhost:${GAIA_PORT}657/net_info | jq -r '.result.peers[] | "\(.node_info.id)@\(.remote_ip):\(.node_info.listen_addr)"' | awk -F ':' '{print $1":"$(NF)}'
   ```
   ## Validator list
   ```bash
   gaiad q staking validators -oj --limit=3000 | jq '.validators[] | select(.status=="BOND_STATUS_BONDED")' | jq -r '(.tokens|tonumber/pow(10; 6)|floor|tostring) + " \t " + .description.moniker' | sort -gr | nl
   ```
   ## Delagate to your validator
   ```bash
  gaiad tx staking delegate $GAIA_VALOPER_ADDRESS 1000000uatom --from=$WALLET --chain-id=$GAIA_CHAIN_ID --fees 250uatom -y
  ```
  ### Commands.
  ```bash
  sudo journalctl -fu gaiad -o cat
  ```
  ```bash
  sudo systemctl restart gaiad
  ```
  ```bash
  sudo systemctl stop gaiad
  ```
  Unjail
  ```bash
  gaiad tx slashing unjail --from $WALLET --chain-id $GAIA_CHAIN_ID --gas=auto 
  ```
  ```bash
  
  ```
  # Delete. 
```bash
sudo systemctl stop gaiad
sudo systemctl disable gaiad
sudo rm /etc/systemd/system/gaiad* -rf
sudo rm $(which gaiad) -rf
sudo rm $HOME/.gaia* -rf
sudo rm $HOME/gaia -rf
sed -i '/GAIA_/d' ~/.bash_profile
```
