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
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash - && \
sudo apt-get install nodejs -y && \
echo -e "\nnodejs > $(node --version).\nnpm  >>> v$(npm --version).\n"
```
