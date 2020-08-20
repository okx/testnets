
* [升级至v0.11.0需要两步](#升级至v0110需要两步)
  * [步骤一：得到最新的genesis.json文件](#步骤一得到最新的genesisjson文件)
     * [方式1：直接下载官方提供的genesis.json](#方式1直接下载官方提供的genesisjson)
     * [方式2：自己migrate出genesis.json（推荐）](#方式2自己migrate出genesisjson推荐)
        * [1. 编译v0.10.10的okchaind](#1-编译v01010的okchaind)
        * [2. 使用v0.10.10的okchaind导出当前genesis.json](#2-使用v01010的okchaind导出当前genesisjson)
        * [3. 使用okchain v0.11.0分支代码，编译新的okchaind](#3-使用okchain-v0110分支代码编译新的okchaind)
        * [4. 使用v0.11.0的 okchaind 执行 migrate，更新genesis.json](#4-使用v0110的-okchaind-执行-migrate更新genesisjson)
  * [步骤二：重启节点](#步骤二重启节点)
     * [1. 使用新的genesis.json重启服务](#1-使用新的genesisjson重启服务)


# 升级至v0.11.0需要两步

## 步骤一：得到最新的genesis.json文件
### 方式1：直接下载官方提供的genesis.json
下载地址：[genesis file](https://raw.githubusercontent.com/okex/testnets/master/v0.11/genesis.json)


### 方式2：自己migrate出genesis.json（推荐）
#### 1. 编译v0.10.10的okchaind
- 切换okchain分支至v0.10.10，编译okchaind，如果
```
git clone https://github.com/okex/okchain.git -b v0.10.10
cd okchain
make install
```

- 查看版本号，确认是v0.10.10
```
okchaind version --long
```

#### 2. 使用v0.10.10的okchaind导出当前genesis.json
- 停掉当前节点
```
# 结束进程
```
- 用官方指定的高度导出genesis.json
```
./okchaind export --for-zero-height --height=9250000 --home /path/to/okchaind --log_level="*:error" > export.json
```
注：--height=9250000 参数必须与官方保持一致。不同的高度会导致export.json不同

- 使用sha256生成摘要，并比对官方的摘要
```
$shasum -a 256 export.json
```
注：官方摘要是


#### 3. 使用okchain v0.11.0分支代码，编译新的okchaind

- 使用最新的okchain v0.11.0分支代码，编译新的okchaind
```
git clone https://github.com/okex/okchain.git -b release/v0.11.0
cd okchain
make GenesisHeight=9250000 install
```
注：GenesisHeight=9250000 参数待最新高度公布后再更新

- 查看版本号，确认是v0.11.0
```
okchaind version --long
```


#### 4. 使用v0.11.0的 okchaind 执行 migrate，更新genesis.json
- 用新的okchaind，执行migrate操作，更新genesis.json
```
okchaind migrate v0.11 /path/to/export.json --chain-id=okchain-testnet1 --genesis-time=2020-08-17T17:00:00Z > genesis.json
```

- 使用sha256生成摘要，并比对官方的摘要
```
$shasum -a 256 genesis.json
```
注：官方摘要是


## 步骤二：重启节点
### 1. 使用新的genesis.json重启服务
- 删除旧数据（或备份）
```
okchaind unsafe-reset-all # 建议先备份，待新网络正常启动后再删除
```
- 将genesis.json复制到/path/to/okchaind/config/目录下
- 重启当前节点







