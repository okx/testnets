# OKC Testnet

This repo collects the genesis, snapshot data and configuration files for the various ExChain
testnets. It exists so the [ExChain repo](https://github.com/okex/exchain)
does not get bogged down with large genesis files and status updates.

## Download the latest testnet data snapshot

 Download URL: 
 
- Download and uncompress the [snapshot](https://static.okex.org/cdn/oec/snapshot/index.html) to exchaind directory
```
export EXCHAIND_PATH=~/.exchaind
rm -rf ${EXCHAIND_PATH}/data
cd ${EXCHAIND_PATH}
wget -c testnet-s0-yyyy-mm-dd-height-rocksdb.tar.gz
tar -zxvf testnet-s0-yyyy-mm-dd-height-rocksdb.tar.gz
```

- Check the snapshot by `ls -l ~/.exchaind/data`
```
total 140
drwxr-xr-x 2 root root 131072 Apr 12 09:14 application.db
drwxr-xr-x 2 root root   4096 Apr 12 09:14 blockstore.db
-rw------- 1 root root     49 Apr 12 09:17 priv_validator_state.json
drwxr-xr-x 2 root root   4096 Apr 12 09:14 state.db
```

## Start with the snapshot
2 ways to startup an exchain full node: 
- start with a docker image
- start with the exchaind binary

### 1. Start testnet with a docker image
- download the docker image
```
docker pull okexchain/fullnode-testnet:latest
```

- run docker based the snapshot downloaded in the previous step `Start based on snapshot`.
```
docker run -d --name exchain-testnet-fullnode -v ~/.exchaind/data:/root/.exchaind/data/ -p 8545:8545 -p 26656:26656 okexchain/fullnode-testnet:latest
```

- view the running log
```
docker logs --tail 100 -f exchain-testnet-fullnode
```

> You can stop the docker container with command: `docker rm -f exchain-testnet-fullnode`
When the docker container gets to the latest block, local RPC can be used：`http://localhost:8545`

___
### 2. Start testnet with the exchaind binary

- Build exchaind by [the latest released version](https://github.com/okex/exchain/releases)
```
make testnet # default is leveldb
make testnet WITH_ROCKSDB=true # if use rocksdb
```

- Initialize exchain node configurations (skip this step if you did it before)
```shell script
exchaind init your_custom_moniker --chain-id exchain-65 --home ~/.exchaind
````

- Start exchaind
```shell script
export EXCHAIN_SEEDS="b7c6bdfe0c3a6c1c68d6d6849f1b60f566e189dd@3.13.150.20:36656,d7eec05e6449945c8e0fd080d58977d671eae588@35.176.111.229:36656,223b5b41d1dba9057401def49b456630e1ab2599@18.162.106.25:36656"
exchaind start --chain-id exchain-65 --home ~/.exchaind --p2p.seeds $EXCHAIN_SEEDS
```






