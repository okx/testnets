
* [2 steps to update to v0.11.0](#2-steps-to-update-to-v0110)
  * [Step 1：Get the latest genesis.json file](#step-1get-the-latest-genesisjson-file)
     * [Method 1：Download genesis.json from the below URL](#method-1download-genesisjson-from-the-below-url)
     * [Method 2：Generate latest genesis.json through okchaind migrate(Recomended)](#method-2generate-latest-genesisjson-through-okchaind-migraterecomended)
        * [1. Compile okchaind v0.10.10](#1-compile-okchaind-v01010)
        * [2. use okchaind v0.10.10 to export genesis.json](#2-use-okchaind-v01010-to-export-genesisjson)
        * [3. Use okchain v0.11.0 code to compile new okchaind](#3-use-okchain-v0110-code-to-compile-new-okchaind)
        * [4. use okchaind v0.11.0 to execute migrate, update genesis.json](#4-use-okchaind-v0110-to-execute-migrate-update-genesisjson)
  * [Step 2：Restart node](#step-2restart-node)
     * [1. Use new genesis.json to restart](#1-use-new-genesisjson-to-restart)




# 2 steps to update to v0.11.0

## Step 1：Get the latest genesis.json file
### Method 1：Download genesis.json from the below URL
Download URL：[genesis file](https://raw.githubusercontent.com/okex/testnets/master/v0.11/genesis.json)


### Method 2：Generate latest genesis.json through `okchaind migrate`(Recomended)
#### 1. Compile okchaind v0.10.10
- Switch okchain branch to v0.10.10, compile okchaind, if
```
git clone https://github.com/okex/okchain.git -b v0.10.10
cd okchain
make install
```

- Check version number, confirm version and commitID
```
okchaind version --long
name: okchain
server_name: okchaind
client_name: okchaincli
version: v0.10.8
commit: cdbfdc8c32292569227d0755f588ddcf45c4364b
build_tags: netgo
go: go version go1.13.12 linux/amd64
cosmos_sdk: v0.37.9
tendermint: v0.32.10
```

#### 2. use okchaind v0.10.10 to export genesis.json
- Stop current node
```
# kill the process
```
- export genesis.json at officially assigned block hight
```
./okchaind export --for-zero-height --height=9460000 --home /path/to/okchaind --log_level="*:error" > export.json
```
Attention：--height=9460000 must correspond with official. Different height will cause different export.json

- Use sha256 to generate abstract and compare it with the official abstract
```
$shasum -a 256 export.json
```
Notice：official abstract is 


#### 3. Use okchain v0.11.0 code to compile new okchaind

- use latest okchain v0.11.0 code to compile new okchaind
```
git clone https://github.com/okex/okchain.git -b v0.11.0
cd okchain
make GenesisHeight=9460000 install
```
Attention：--height=9460000 must correspond with official.

- Check version number, confirm version and commitID
```
okchaind version --long
name: okchain
server_name: okchaind
client_name: okchaincli
version: v0.11.0
commit: 808fa9b55530affc7a3a1a1bb8384c58eb6d3512
build_tags: netgo
go: go version go1.14.2 darwin/amd64
cosmos_sdk: v0.37.9
tendermint: v0.32.10
```


#### 4. use okchaind v0.11.0 to execute migrate, update genesis.json
- use new okchaind to execute migrate and update genesis.json
```
okchaind migrate v0.11 /path/to/export.json --chain-id=okchain-testnet1 --genesis-time=2020-08-17T17:00:00Z > genesis.json
```

- Use sha256 to generate abstract and compare it with the official abstract
```
$shasum -a 256 genesis.json
```
Notice：official abstract is


## Step 2：Restart node
### 1. Use new genesis.json to restart
- delete old data (or back up)
```
okchaind unsafe-reset-all # recommend to back up first, delete the old data after the new network restart successfully
```
- copy genesis.json to /path/to/okchaind/config/
- Restart current node
