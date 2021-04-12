# OKExChain Testnet

This repo collects the genesis, snapshot data and configuration files for the various OKChain
testnets. It exists so the [OKExChain repo](https://github.com/okex/exchain)
does not get bogged down with large genesis files and status updates.

## Getting Started

[Getting Started Docs](https://okexchain-docs.readthedocs.io/en/latest/getting-start/join-okexchain-testnet.html)

## Download the latest testnet data snapshot

 Download URL: 
 
- Download and uncompress the [snapshot](https://ok-public-hk.oss-cn-hongkong.aliyuncs.com/cdn/okexchain/snapshot/data_170.tar.gz) to okexchaind directory
```
mv ~/.okexchaind/data ~/.okexchaind/data-bak
cd ~/.okexchaind git
wget -c https://ok-public-hk.oss-cn-hongkong.aliyuncs.com/cdn/okexchain/snapshot/data_170.tar.gz
tar -zxvf data_170.tar.gz
```

- Check the snapshot by `ls -l ~/.okexchaind/data`
```
total 8
drwxr-xr-x  1026 oak  staff  32832 Mar  7 09:20 application.db
drwxr-xr-x    10 oak  staff    320 Mar  7 09:19 blockstore.db
drwx------     3 oak  staff     96 Mar  5 18:43 cs.wal
drwxr-xr-x     8 oak  staff    256 Mar  7 09:19 evidence.db
-rw-------     1 oak  staff     48 Mar  7 09:17 priv_validator_state.json
drwxr-xr-x    12 oak  staff    384 Mar  7 09:20 state.db
drwxr-xr-x     9 oak  staff    288 Mar  7 09:19 tx_index.db
```

## Start with the snapshot
2 ways to startup an okexchain full node: 
- start with a docker image
- start with the okexchaind binary

### 1. Start testnet with a docker image
- download the docker image
```
docker pull okexchain/fullnode-testnet:latest
```

- run docker based the snapshot downloaded in the previous step `Start based on snapshot`.
```
docker run -d --name okexchain-testnet-fullnode -v ~/.okexchaind/data:/root/.okexchaind/data/ -p 8545:8545 okexchain/fullnode-testnet:latest
```

- view the running log
```
docker logs --tail 100 -f okexchain-testnet-fullnode
```

> You can stop the docker container with command: `docker stop okexchain-testnet-fullnode`, and restart the docker container with command: `docker start okexchain-testnet-fullnode`. 
When the docker container gets to the latest block, local RPC can be used：`http://localhost:8545`

___
### 2. Start testnet with the okexchaind binary

- Build okexchaind by [the latest released version v0.17.1](https://github.com/okex/exchain/releases/tag/v0.17.1)
```
make GenesisHeight=1121818 install
```

- Initialize okexchain node configurations (skip this step if you did it before)
```shell script
okexchaind init your_custom_moniker --chain-id okexchain-65 --home ~/.okexchaind
````

- Start okexchaind
```shell script
export OKEXCHAIN_SEEDS="b7c6bdfe0c3a6c1c68d6d6849f1b60f566e189dd@3.13.150.20:36656,d7eec05e6449945c8e0fd080d58977d671eae588@35.176.111.229:36656,223b5b41d1dba9057401def49b456630e1ab2599@18.162.106.25:36656"
okexchaind start --chain-id okexchain-65 --home ~/.okexchaind --p2p.seeds $OKEXCHAIN_SEEDS
```






