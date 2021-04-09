
# OKExChain 测试网V0.17.0升级公告


尊敬的OKExChain社区用户：

我们将在2021/04/10 07:00 UTC对测试网进行升级，此次升级不清数据，chain-id不变，仍是`okexchain-65`，以下为升级公告内容：

## OKExChain测试网V0.17.0升级内容
1. 原来测试网地址前缀是okexchain，新测试网更改为ex。
2. 进行了一些优化和修复了一些bug。详情见：https://github.com/okex/okexchain/releases/tag/v0.17.0


## 作为OKExChain验证人，我需要做些什么？
本次升级不清数据升级。请于2021/04/10 07:00 UTC前停掉当前测试网运行节点，使用新数据快照替换掉原有数据。
创建测试网教程请参考下面链接：
https://github.com/okex/testnets

## 钱包、区块浏览器、其他服务提供商，分别需要做什么？
因原okexchain地址更新为ex前缀地址，需要升级至最新的sdk，以连接最新的区块链网络。

okexchain-go-sdk更新到v0.17.0：  
https://github.com/okex/okexchain-go-sdk/releases

okexchain-java-sdk更新到v0.17.0：  
https://github.com/okex/okexchain-java-sdk/releases

okexchain-javascript-sdk更新到v0.17.0：  
https://github.com/okex/okexchain-javascript-sdk/releases

## 对测试网用户有什么影响
1. 因测试网地址前缀更改，由原来的地址变成全新的ex开头地址。私钥不变，无需担心资产丢失。  
2. 对于dex网页钱包和三方钱包，在未更新适配新地址前，测试网暂无法使用转账，swap和dex等功能，但不影响通过metamask调用智能合约。



与往常一样，在管理任何加密货币时，请使用适当的操作程序，并警惕网络钓鱼和其他的利用手段。
您可参考的可靠消息来源是以下OKExChain团队提供的3条渠道，面向用户的官方OKExChain交流渠道。
以下是传达升级详细信息的官方账户：
- OKExChian GitHub存储库：https://github.com/okex/okexchain
- OKExChain博客：https://www.okex.com/academy/zh/category/okexchain/
- Telegram group：https://t.me/okexchaintech 

如果您对接下来要采取的步骤有疑问或困惑，并且不确定信息来源是否可靠，那么请不要在初始阶段进行任何操作，耐心等待上面列出的三个通信渠道的更新。请勿向任何管理员，网站或非官方软件提供你的12位助记词。  


OKExChain社区  
2021年04月10日






