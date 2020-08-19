# 升级步骤
### 1. 生成v0.10.10的okchaind
- 切换okchain分支至v0.10.10，生成okchaind
```
cd okchain
git checkout release/v0.10.10
git pull
make install
```

### 2. 使用v0.10.10的okchaind export出旧genesis.json
- 停掉当前节点
```
# 结束进程
```
- 用okchaind（v0.10.10）导出genesis.json
```
./okchaind export --for-zero-height --height=9190000 --home /data/okchain_data/val16/okchaind --log_level="*:error" > export.json
```
注1：指定高度，前100或1万的整数倍的高度。  
注2：导出需要1分钟左右

- 使用sha256生成摘要，并比对官方的摘要
```
$shasum -a 256 genesis.json
```


### 3. 使用okchain v0.11.0分支，生成新的okchaind

- 下载最新的okchain v0.11.0版本代码，生成新的okchaind
```
cd okchain
git checkout v0.11.0
git pull
make install
```
- 查看版本号，确认是v0.11.0
```
okchaind version --long
```


### 4. 使用v0.11.0的 okchaind 执行 migrate，更新genesis.json
- 用新的okchaind，执行migrate操作，更新genesis.json
```
mv genesis.json export.json
okchaind migrate v0.11 /path/to/export.json --chain-id=okchain-testnet1 --genesis-time=2020-08-17T17:00:00Z > genesis.json
```
- 使用sha256生成摘要，并比对官方的摘要
```
$shasum -a 256 genesis.json
```

### 5. 使用新的genesis.json重启服务
- 删除旧数据（或备份）
- 将genesis.json复制到~/okchaind/config/目录下
- 重启







