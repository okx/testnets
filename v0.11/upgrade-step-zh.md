
* [升级至v0.11.1需要两步](#升级至v0110需要两步)
  * [步骤一：得到最新的genesis.json文件](#步骤一得到最新的genesisjson文件)
     * [方式1：直接下载官方提供的genesis.json](#方式1直接下载官方提供的genesisjson)
     * [方式2：通过`okchaind migrate`生成最新的genesis.json(推荐)](#方式2自己migrate出genesisjson推荐)
        * [1. 编译v0.10.10的okchaind](#1-编译v01010的okchaind)
        * [2. 使用v0.10.10的okchaind导出当前genesis.json](#2-使用v01010的okchaind导出当前genesisjson)
        * [3. 使用okchain v0.11.1分支代码，编译新的okchaind](#3-使用okchain-v0110分支代码编译新的okchaind)
        * [4. 使用v0.11.0的 okchaind 执行 migrate，更新genesis.json](#4-使用v0110的-okchaind-执行-migrate更新genesisjson)
  * [步骤二：重启节点](#步骤二重启节点)
     * [1. 使用okchain v0.11.1分支代码，编译新的okchaind](#1-使用okchain-v0111分支代码编译新的okchaind)
     * [2. 使用新的genesis.json重启服务](#2-使用新的genesisjson重启服务)


# 升级至v0.11.1需要两步

## 步骤一：得到最新的genesis.json文件
### 方式1：直接下载官方提供的genesis.json
下载地址：[genesis file](https://raw.githubusercontent.com/okex/testnets/master/v0.11/genesis.json)  

### 方式2：通过`okchaind migrate`生成最新的genesis.json(推荐)
#### 1. 编译v0.10.10的okchaind
- 切换okchain分支至v0.10.10，编译okchaind
```
git clone https://github.com/okex/okchain.git -b v0.10.10
cd okchain
make install
```

- 查看版本号，确认是版本和commitID
```
okchaind version --long

name: okchain
server_name: okchaind
client_name: okchaincli
commit: cdbfdc8c32292569227d0755f588ddcf45c4364b
build_tags: netgo
go: go version go1.13.12 linux/amd64
cosmos_sdk: v0.37.9
tendermint: v0.32.10
```

#### 2. 使用v0.10.10的okchaind导出当前genesis.json
- 停掉当前节点
```
# 结束进程
```
- 用官方指定的高度9450000导出genesis.json
```
./okchaind export --for-zero-height --height=9450000 --home /path/to/okchaind --log_level="*:error" > export.json
```
注：--height=9450000 参数必须与官方保持一致。不同的高度会导致export.json不同

- 使用sha256生成摘要，并比对官方的摘要
```
$shasum -a 256 export.json
821e69f0b64e06fc75e1fac804f837236a37ac6c1ba9902b8a74a30f275c1241
```


#### 3. 使用okchain v0.11.1分支代码，编译新的okchaind

- 使用最新的okchain v0.11.1分支代码，编译新的okchaind
```
git clone https://github.com/okex/okchain.git -b v0.11.1
cd okchain
make GenesisHeight=9450000 install
```
注：GenesisHeight=9450000 参数必须与官方保持一致。

- 查看版本号，确认版本和commitID
```
okchaind version --long

name: okchain
server_name: okchaind
client_name: okchaincli
version: v0.11.1
commit: 64be77515eb35af1db5a4365990cb22d201230fb
build_tags: netgo
go: go version go1.14.2 darwin/amd64
cosmos_sdk: v0.37.9
tendermint: v0.32.10
```


#### 4. 使用v0.11.1的 okchaind 执行 migrate，更新genesis.json
- 用新的okchaind，执行migrate操作，更新genesis.json
```
okchaind migrate v0.11 /path/to/export.json --chain-id=okchain-testnet1 --genesis-time=2020-08-26T04:55:00Z > genesis.json
```
注：本次的chain-id=okchain-testnet1

- 使用sha256生成摘要，并比对官方的摘要
```
$shasum -a 256 genesis.json
d80e2a234c01a5f4690f9f76341f22db7d913181c28a51a2fb02082fd90b9a97
```


## 步骤二：重启节点

### 1. 使用okchain v0.11.1分支代码，编译新的okchaind
[编译方法](https://github.com/okex/testnets/blob/master/v0.11/upgrade-step-zh.md#3-%E4%BD%BF%E7%94%A8okchain-v0111%E5%88%86%E6%94%AF%E4%BB%A3%E7%A0%81%E7%BC%96%E8%AF%91%E6%96%B0%E7%9A%84okchaind)


### 2. 使用新的genesis.json重启服务
- 删除旧数据（或备份）
```
okchaind unsafe-reset-all # 建议先备份，待新网络正常启动后再删除
```
- 将genesis.json复制到/path/to/okchaind/config/目录下
- 重启当前节点
```
okchaind start # 使用v0.11.1的 okchaind
```






