# OKEx Upgrades OKExChain Testnet to V0.17.0


Dear OKExChain community members:

OKExChain is scheduled to upgrade its testnet to V0.17.0 at 2021/04/10 07:00 UTC, previous data won't be deleted and the chain-id remains `okexchain-65`, below are the details

## OKExChain testnet v0.17.0 upgrades details
1. Prefix of testnet address change from okexchain to ex.
2. Some bug fixed and improvements: https://github.com/okex/okexchain/releases/tag/v0.17.0


## What are the duties of an OKExChain validator?
Please stop the current testnet node before 2021/04/10 07:00 UTC, restart a node and replace the previous data with new snapshot to join the new testnet. 
Instructions: https://github.com/okex/testnets


## How can wallets, block browsers and other service providers support the network upgrade?
Because prefix of testnet address change from okexchain to ex, please upgrade to latest sdk and join the new testnet.
okexchain-go-sdk upgrade to v0.17.0：  
https://github.com/okex/okexchain-go-sdk/releases

okexchain-java-sdk upgrade to v0.17.0：   
https://github.com/okex/okexchain-java-sdk/releases

okexchain-javascript-sdk upgrade to v0.17.0：  
https://github.com/okex/okexchain-javascript-sdk/releases


## What's the influences to testnet users?
1. Because prefix of testnet address changed, the previous address will be changed to a totally new address with ex prefix.
2. The private key remains unchanged, so no worries about asset loss.

Before dex web wallet and third party wallets upgrade to adopt the new address with ex prefix, users can not use testnet functions like transfer, swap and dex. But you can still use metamask to invoke smart contract.


Users in the app may suffer a short service outage. The duration of the outage depends on the application used. To provide a solid user experience, service providers should adopt appropriate operating procedures and be aware of potential phishing attacks.
Please refer to OKExChain's official channels, listed below, for updated and accurate information.
- OKExChian GitHub：https://github.com/okex/okexchain
- OKExChain Blog：https://www.okex.com/academy/en/category/okexchain-en/
- Telegram group：https://t.me/okexchaintech 

If you have any doubts about the steps of the network upgrade and the reliability of the information, please wait for instructions from OKExChain's official channels before taking any actions. Please do not provide your 12-digits passwords to any administrator, website or unofficial software.

OKExChain  
2021/04/10
