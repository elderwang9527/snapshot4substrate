# substrate快照工具

[English version](https://github.com/playdog-io/snapshot4substrate/blob/main/README_zh.md)

只需拥有一个全节点数据，就能使用此工具快速获取一条substrate链上的所有账户地址余额，从而可以很轻松的根据余额信息重启一条链。如你想了解具体原理，可以参考此文章：https://www.shawntabrizi.com/substrate/transparent-keys-in-substrate

## 使用步骤

1
```
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "state_getKeys", "params": ["0x26aa394eea5630e07c48ae0c9558cef7b99d880ec681799c0cf30e8886371da9"]}' http://localhost:1234 > keys_raw.json
```
在运行节点的服务器上执行以上命令，注意1234替换为节点的rpc端口。

2
![](images/2021-07-19-17-11-26.png)
左图所示，将得到的如左图所示的keys_raw.json文件的所有字段保留左侧的0x和右侧的共64个字符，删掉中间的所有字符。得到如右图所示的keys.json文件。

3  
![](images/2021-07-19-17-39-16.png)
编辑snapshot.js文件：
a，将之得到的keys.json文件复制粘贴到var = hex后。   
b，将wss://rpc.subplay.xyz 替换为目标链的wss接口。    
c，将for循环中的数字448替换为keys.json中的条目总数-1。    

4

