# 用户一键下单

## 获取取件时间

### URL

/order/c/order/picking_time/

### HTTP请求方式

__GET__

### HTTP请求参数

| 参数名称 | 参数类型 | 参数描述   |
| -------- | -------- | ---------- |
| user_sid | String   | 16位会话ID |

### HTTP响应参数

| 参数名称     | 参数类型 | 参数描述     |
| ------------ | -------- | ------------ |
| result       | Int      | 请求结果     |
| picking_time | List     | 预约时间列表 |

### API 注释

result含义：

| 值   | 意义            |
| ---- | --------------- |
| 200  | 请求成功        |
| 404  | user_sid 不存在 |
| 500  | 未知错误        |

### 示例

__请求__

```http
GET /order/c/order/picking_time/?user_sid=12312312xxxxxx
```

__响应__

```json
{
    "response": {
        "result": 200,
        "picking_time": [
            {
                "day": "今天",
                "time_list": [
                    {
                        "time": "随时",
                        "order_picking_time": 0
                    },
                    {
                        "time": "8:00-12:00",
                        "order_picking_time": 1,
                    }, ...
                ]
            },
            {
                "day": "明天",
                "time_list": [
                    {
                        "time": "随时",
                        "order_picking_time": 6,
                    }, ...
                ]
			}, ...
        ]
    }
}
```

## 一键下单

### URL

/order/c/order/

### HTTP请求方式

__POST JSON__

### HTTP请求参数

| 参数名称           | 参数类型 | 参数描述            |
| ------------------ | -------- | ------------------- |
| user_sid           | String   | 16位会话ID          |
| customer_appraisal | List     | 列表-数目组成的列表 |
| order_picking_time | Int      | 取件时间标识        |
| deli_id            | Int      | 用户的收货地址id    |

### HTTP响应参数

| 参数名称   | 参数类型                               | 参数描述 |
| ---------- | -------------------------------------- | -------- |
| result     | Int                                    | 请求结果 |
| order_info | [OrderInfo](/Model/order/order-model/) | 订单模型 |

### API 注释

result含义：

| 值   | 意义                   |
| ---- | ---------------------- |
| 200  | 请求成功               |
| 402  | deli_id错误            |
| 403  | 该用户还存在未完成订单 |
| 404  | user_sid 不存在        |
| 500  | 未知错误               |

### 示例

__请求__

```json
{
	"data":{
		"user_sid": "3fd60833-f543-11e8-9057-6c96cfdf6ce7",
		"customer_appraisal":[
			{
                "p_type": 1,
                "quantity": 30,
                "quantity_max": 60,
            },
            {
                "p_type": 2,
                "quantity": 120,
                "quantity_max": null,
            }
        ],
        "deli_id": 9
	}
}
```

__响应__



## 一键下单（旧版）

### URL
/order/operate/one_click_order/

### HTTP请求方式
__POST JSON__


### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			    | String 	            | 16位会话ID
type_quantity           | List                  | 列表-数目组成的列表
deli_id                 | Int                   | 用户的收货地址id


### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
result					| Int					| 请求结果
order_info              | [OrderInfo](/Model/order/order-model/) | 订单模型

### API 注释

result含义：

值		|意义
--------|--------
200		|请求成功
402     |deli_id错误
403     |该用户还存在未完成订单
404		|user_sid 不存在
500		|未知错误

### 示例

__请求__
```json
{
	"data":{
		"user_sid": "3fd60833-f543-11e8-9057-6c96cfdf6ce7",
		"type_quantity":[
			{
			"p_type": 1,
			"quantity": 10
            },
            {
                "p_type": 2,
                "quantity": 100
            }
        ],
        "deli_id": 9
	}
}
```

__响应__

```json
{
    "version": "0.1",
    "response": {
        "result": 200,
        "order_info": {
            "location": "北京市海淀区xxxx",
            "id": 20,
            "create_time": "2018-12-03T19:18:17.787843+08:00",
            "o_state": 0,
            "c_delivery_info": {
                "id": 9,
                "address": "北京市海淀区xxxx",
                "contact": "张xx",
                "house_number": "307",
                "contact_pn": "13800138000"
            }
        }
    },
    "context": null
}
```