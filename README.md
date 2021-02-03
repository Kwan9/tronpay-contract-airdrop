## 波场空投合约

### 说明

本质上就是批量转 TRX / 批量转 token。比如批量提现，空投等场景。

### 使用

> 以 USDT.TRC20 批量转账为例：

1.　首先初始化 USDT.TRC20 合约实例。

```
    // USDT.TRC20 的合约地址
    const usdtContractAddress = "TR7NHqjeKQxGTCi8q8ZY4pL8otSzgjLj6t"; 

    // 通过 tronWeb 初始化合约
    const usdtContractInstance = await tronWeb.contract().at(usdtContractAddress);
```

2.　然后进行转账授权，即调用合约的 ```approve``` 方法。

```
    // 空投合约的合约地址
    const multiContractAddress = "TG9rv435qUKmPaT8fPbb9jBhhS3sEZ6XxP";

    // 授权
    await usdtContractInstance.approve(
        multiContractAddress, // 
        10000,　// 这里是批量转的累计金额
    ).send();
```

3. 初始化空投合约

```
    // 空投合约的合约地址
    const multiContractAddress = "TG9rv435qUKmPaT8fPbb9jBhhS3sEZ6XxP";

    // 通过 tronWeb 初始化合约
    const multiContractInstance = await tronWeb.contract().at(multiContractAddress);
```

3. 调用空投合约的方法进行批量转账

```

    // mulSendAddresses、mulSendAmounts 分别为接收地址列表及转账金额列表。数组格式。

    const res = await multiContractInstance.sendToken(
        usdtContractAddress,
        mulSendAddresses,
        mulSendAmounts
    ).send({
        feeLimit: 2000000
    });
```


