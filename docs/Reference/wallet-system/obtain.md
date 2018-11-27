# 获取余额和明细

## 获取用户余额

### URL
/wallet/obtain/balance/

### HTTP请求方式
__GET__


### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			     		| String 	    | 16位会话ID

### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
balance 			  	| Float 				| 用户余额
result					| Int					| 登录结果

### API 注释

result含义：

值		|意义
--------|--------
200		|请求成功
404		|user_sid 不存在
500		|未知错误

### 示例

__请求__

/wallet/obtain/balance/?user_sid=f4bd5621-f196-11e8-bb37-6c96cfdf6ce7
__响应__

```json
{
    "version": "0.1",
    "response": {
        "balance": 23,
        "result": 200
    },
    "context": null
}
```
--------------------------------------

## 获取余额明细

### URL
/wallet/obtain/history/

### HTTP请求方式
__GET__


### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			     		| String 	    | 16位会话ID
page                    | Int                   | 指定明细的页数，不传则默认为0

### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
n_pages 			  	| Int    				| 总页数
history                 | List of [TransactionDetail](/Model/wallet/wallet-model/) | 明细列表
result					| Int					| 登录结果


### API 注释

result含义：

值		|意义
--------|--------
200		|请求成功
400     |请求错误或page超出总页数
404		|user_sid 不存在
500		|未知错误

### 示例

__请求__

/wallet/obtain/history/?user_sid=f4bd5621-f196-11e8-bb37-6c96cfdf6ce7&page=0

__响应__

```json
{
    "version": "0.1",
    "response": {
        "n_pages": 1,
        "result": 200,
        "history": [
            {
                "id": 3,
                "create_time": "2018-11-27T21:02:03.114365+08:00",
                "transaction_type": 2,
                "amount": 12,
                "oid": null,
                "uid": 1
            },
            {
                "id": 2,
                "create_time": "2018-11-27T00:45:48.692503+08:00",
                "transaction_type": 1,
                "amount": 1,
                "oid": null,
                "uid": 1
            }
        ]
    },
    "context": null
}
```