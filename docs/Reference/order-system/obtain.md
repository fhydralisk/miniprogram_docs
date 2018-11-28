# 我的投递

## 获取累积投递次数和累积赚取金额

### URL
/order/obtain/overview/

### HTTP请求方式
__GET__


### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			     		| String 	    | 16位会话ID

### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
n_times 			  	| Int    				| 投递次数
total_amount            | Float                 | 累积赚取
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

/order/obtain/overview/?user_sid=a81966ab-f2da-11e8-900b-6c96cfdf6ce7

__响应__

```json
{
    "version": "0.1",
    "response": {
        "n_times": 3,
        "result": 200,
        "total_amount": 10.1
    },
    "context": null
}
```
--------------------------------------

## 获取投递列表

### URL
/order/obtain/order_list/

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
oeders                 | List of [OrderInfo](/Model/order/order-model/) | 投递列表
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

/order/obtain/order_list/?user_sid=a81966ab-f2da-11e8-900b-6c96cfdf6ce7&page=0

__响应__

```json
{
    "version": "0.1",
    "response": {
        "n_pages": 1,
        "result": 200,
        "orders": [
            {
                "id": 4,
                "create_time": "2018-11-28T15:33:28.766459+08:00",
                "location": "海淀区大钟寺金典小区",
                "amount": 10.6,
                "o_state": 2,
                "uid": 1
            },
            {
                "id": 3,
                "create_time": "2018-11-28T15:04:01.392396+08:00",
                "location": "海淀区大钟寺金典小区",
                "amount": 10.1,
                "o_state": 3,
                "uid": 1
            }
        ]
    },
    "context": null
}
```