# 订单相关接口（2.0）

## 获取订单详情

查看订单详情，订单记账的汇总聚合，以及订下单所在位置与当前地点的距离（仅B端）

### URL

*B端*

GET /order/b/order/

*C端*

GET /order/c/order/

### 请求参数

| 参数名称 | 参数类型                                 | 参数说明 |
| -------- | ---------------------------------------- | -------- |
| oid      | FK OrderInfo                             | 订单id   |
| agg_op   | String(aggregate_operation_choice)(可选) | 聚合方式 |
| lat      | Decimal(可选)                            | 纬度     |
| lng      | Decimal(可选)                            | 经度     |
| user_sid |                                          |          |

### 应答

| 字段名称   | 字段类型                                                    | 字段说明     |
| ---------- | ----------------------------------------------------------- | ------------ |
| order      | [OrderView](/View/order/order/)                             | 订单详情     |
| distance   | Float                                                       | 距离（公里） |
| aggregates | [OrderBookkeepingAggregateListView](/View/order/aggregate/) | 订单聚合视图 |

### 注释

*agg_op*

| 值             | 说明                           |
| -------------- | ------------------------------ |
| subtype_b      | 按2级品类汇总，返回B端顶级品类 |
| subtype_c      | 按2级品类汇总，返回C端顶级品类 |
| toptype_b      | 按B端1级品类汇总               |
| toptype_b_unit | 按B端1级品类及单位汇总         |
| toptype_c      | 按C端1级品类汇总               |
| toptype_c_unit | 按C端1级品类及单位汇总         |
| unit           | 按单位汇总                     |

例如，选择agg_op=toptype_b_unit，则统计记账中1级品类中各个单位的价格、数量；选择agg_op=unit则只统计各单位的数量、价格，忽略品类。

### 请求示例

```http
GET /order/b/order/?oid=636&user_sid=tttaaa&agg_op=toptype_b_unit
```

### 应答示例

```json
{
    "version": "2.0",
    "response": {
        "distance": null,
        "aggregates": {
            "aggregates": [
                {
                    "quantity": "1.000000",
                    "price": "1.000",
                    "top_type": {
                        "id": 28,
                        "t_top_name": "杂料(塑)",
                        "in_use": true
                    },
                    "unit": 1
                }
            ],
            "total_price": "1.000"
        },
        "result": 200,
        "order": {
            "id": 636,
            "create_time": 1551886890,
            "grab_time": 1551886890,
            "complete_time": 1551886890,
            "o_state": 3,
            "amount": "1.000",
            "c_delivery_info": null,
            "recycling_staff": {
                "rs_name": "张三",
                "rs_pn": "18888888888"
            },
            "time_remain": 0,
            "time_remain_b": 0,
            "target_time": 1551890490,
            "order_picking_time": null,
            "can_cancel_b": true,
            "budget": null,
            "delete_code": 0,
            "bookkeeping": [
                {
                    "quantity": "1.000000",
                    "sub_type": {
                        "id": 91,
                        "unit": 1,
                        "t_sub_name": "白料",
                        "in_use": true,
                        "price_default_flow": "1.900",
                        "price_default_fix": "2.200",
                        "toptype_b": {
                            "id": 28,
                            "t_top_name": "杂料(塑)",
                            "in_use": true,
                            "description": ""
                        },
                        "toptype_c": {
                            "id": 24,
                            "t_top_name": "其他塑料",
                            "in_use": true,
                            "description": ""
                        }
                    },
                    "price": "1.000"
                }
            ],
            "customer_products": []
        }
    },
    "context": null
}
```

### 接口替换

本接口替换如下原有接口

| URL                                   | 备注 |
| ------------------------------------- | ---- |
| /order/obtain/order_details_b/        |      |
| /order/obtain/order_details_c/        |      |
| /order/c/detail/detail/               |      |
| /order/detail/final_t_p_detail/       |      |
| /order/obtain/order_details_customer/ |      |

--------

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
    "user_sid": "3fd60833-f543-11e8-9057-6c96cfdf6ce7",
	"data":{
        "order_picking_time": 0,
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