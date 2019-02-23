# 宝宝金余额

## 获取用户余额

### URL
/wallet/balance/

### HTTP请求方式
__GET__

### HTTP请求参数

无（但需要提交user_sid）

### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
balance 			  	| Decimal | 用户余额
balance_freezing | Decimal | 冻结余额 
result					| Int					| 请求结果

### API 注释

result含义：

值		|意义
--------|--------
200		|请求成功
404		|user_sid 不存在
500		|未知错误

### 示例

__请求__

```http
GET /wallet/balance/?user_sid=f4bd5621-f196-11e8-bb37-6c96cfdf6ce7
```


__响应__

```json
{
    "version": "0.1",
    "response": {
        "balance": "23.000",
        "balance_freezing": "10.000",
        "result": 200
    },
    "context": null
}
```
--------------------------------------
