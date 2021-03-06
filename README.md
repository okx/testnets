# OKExChain Testnets

This repo collects the genesis and configuration files for the various OKChain
testnets. It exists so the [OKExChain repo](https://github.com/okex/okexchain)
does not get bogged down with large genesis files and status updates.

## Getting Started

To get started with the latest testnet, see the
[docs](https://okexchain-docs.readthedocs.io/en/latest/getting-start/join-okexchain-testnet.html).

## Testnet Status

Source Code: [latest released version v0.16.8](https://github.com/okex/okexchain/releases/tag/v0.16.8)

Build latest released okexchaind 
```
make GenesisHeight=1121818 install
```

## Seed

Seed nodes:
```
b7c6bdfe0c3a6c1c68d6d6849f1b60f566e189dd@3.13.150.20:36656
d7eec05e6449945c8e0fd080d58977d671eae588@35.176.111.229:36656
223b5b41d1dba9057401def49b456630e1ab2599@18.162.106.25:36656
```

## Start based on snapshot

Download the [snapshot](https://ok-public-hk.oss-cn-hongkong.aliyuncs.com/cdn/okexchain/snapshot/okexchain-v0.16.8-testnet-20210305-height_1121961.tar.gz)

Unpack the snapshot data to okexchaind directory
```
mv ~/.okexchaind/data ~/.okexchaind/data-bak
cd ~/.okexchaind 
wget -c https://ok-public-hk.oss-cn-hongkong.aliyuncs.com/cdn/okexchain/snapshot/okexchain-v0.16.8-testnet-20210305-height_1121961.tar.gz
tar -zxvf okexchain-v0.16.8-testnet-20210305-height_1121961.tar.gz
```

## Start with docker
### 1. download the docker image
```
docker pull okexchain/fullnode-testnet:latest
```

### 2. run docker based the snapshot downloaded in the previous step `Start based on snapshot`.
```
docker run -d --name okexchain-testnet-fullnode -v ~/.okexchaind/data:/root/.okexchaind/data/ -p 8545:8545 okexchain/fullnode-testnet:latest
```

### 3. view the running log
```
docker logs --tail 100 -f okexchain-testnet-fullnode
```


> You can stop the docker container with command: `docker stop okexchain-testnet-fullnode`, and restart the docker container with command: `docker start okexchain-testnet-fullnode`. 
When the docker container gets to the latest block, local RPC can be used：`http://localhost:8545`