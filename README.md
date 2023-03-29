# OKC Testnet

This repo collects the genesis, snapshot data and configuration files for the various OKC
testnets. It exists so the [OKC repo](https://github.com/okex/exchain)
does not get bogged down with large genesis files and status updates.

## Download the latest testnet data snapshot

There are 3 types of snapshots and s0 is the one with minimum data size:
- s0: the most recent block and world state
- s1: all historical blocks and the most recent world state
- s3: all historical blocks and world states

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
make testnet # default is rocksdb, you may need to execute "make rocksdb" first
make testnet WITH_ROCKSDB=false # if use leveldb
```

- Initialize exchain node configurations (skip this step if you did it before)
```shell script
exchaind init your_custom_moniker --chain-id exchain-65 --home ~/.exchaind
````

- Start exchaind
```shell script
exchaind start --chain-id exchain-65 --home ~/.exchaind
```






