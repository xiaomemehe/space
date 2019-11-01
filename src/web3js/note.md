* 版本 v1.2.2  地址：https://web3js.readthedocs.io/en/v1.2.2/web3-eth.html#gettransactionreceipt
* 注意：和版本区别可能会出现函数区别，比如：web3.eth.sendRawTransaction在v1.2.2中不可用，变为web3.eth.sendSingleTransaction
* 对ethereumjs-tx的require，在交易中 需要Tx = require('ethereumjs-tx').Transaction;同时实例化的时候 new Tx(rawTx,{ chain: 'rinkeby'});文档中有体现
```
var rawTx = {
            nonce: '0x'+_number,//随机数
            //gasPrice和gasLimit如果不知道怎么填，可以参考etherscan上的任意一笔交易的值
            gasPrice: '0x'+_gasPrice,
            gasLimit: '0x295f05',
            to: '0x29328A9349c38c312e2F713CC12f6EB3a0dE3230',//接受方地址或者合约地址
            value: '0x'+_value,//发送的金额，这里是16进制，实际表示发送1个wei
            data: ''
        };
```
* 交易数量 为 交易的实际数量（value）加上手续费（gasPrice*gasLimit--不一定是设置的值，具体看getTransaction中的gasPrice和getTransactionReceipt中的gasUsed: 21000（最小为这个值）,）
