# 取消订单

## 获取取消理由列表

### URL

/order/obtain/cancel_reason/

### HTTP请求方式
__GET__


### HTTP请求参数
无


### HTTP响应参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
reasons                 | List                  | 取消原因列表
result					| Int					| 登录结果


### API 注释

result含义：

值		|意义
--------|--------
200		|请求成功
500		|未知错误

### 示例

__请求__

http://127.0.0.1:8000/order/obtain/cancel_reason/

__响应__

```json
{
    "version": "0.1",
    "response": {
        "reasons": [
            {
                "id": 1,
                "reason": "原因1"
            },
            {
                "id": 2,
                "reason": "原因2"
            },
            {
                "id": 3,
                "reason": "原因3"
            }
        ],
        "result": 200
    },
    "context": null
}
```
--------------------------
## 取消订单

### URL

/order/operate/cancel_order/

### HTTP请求方式
__POST   JSON__


### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid                | String                  | 128位会话id
reason                  | Int                   | 取消理由id
order                   | Int                   | 订单id
desc                    | String                | 其他理由
result					| Int					| 登录结果

**reason和desc至少有一个不能为空**


### HTTP响应参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
result					| Int					| 登录结果


### API 注释

result含义：

值		|意义
--------|--------
200		|请求成功
402     | reason和desc都为空
403     | 该订单不能进行该操作
500		|未知错误

### 示例

__请求__

```json
{
    "data": {
	"user_sid": "3fd60833-f543-11e8-9057-6c96cfdf6ce7",
	"reason": 1,
	"order": 10,
	"desc": "不想卖"
    }
}
```

__响应__

```json
{
    "version": "0.1",
    "response": {
        "result": 200
    },
    "context": null
}
```
