# 订单相关接口（2.0）

## 获取订单详情

查看订单详情，订单记账的汇总聚合，以及订下单所在位置与当前地点的距离（仅B端）

### URL

*B端*

GET /order/b/order/

*C端*

GET /order/c/order/

### 请求参数

| 参数名称 | 参数类型                                                     | 参数说明 |
| -------- | ------------------------------------------------------------ | -------- |
| oid      | FK OrderInfo                                                 | 订单id   |
| agg_op   | [AggOperationChoice](/View/order/aggregate/#aggoperationchoice)(可选) | 聚合方式 |
| lat      | Decimal(可选)                                                | 纬度     |
| lng      | Decimal(可选)                                                | 经度     |
| user_sid |                                                              |          |

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

------

## 获取订单列表

### URL

*B端*

GET /order/b/order/list/

### HTTP 请求参数

| 参数名称   | 类型                              | 含义       |
| ---------- | --------------------------------- | ---------- |
| user_sid   |                                   |            |
| to_grab    | Boolean                           | 获取待抢订单列表 |
| load_id    | PK of LoadingCredential           | 装车单ID |
| start_time | Timestamp                         | 订单创建时间范围-起始 |
| end_time   | Timestamp                         | 订单创建时间范围-终止 |
| o_states   | List of [o_state_choice](/View/order/order/#order_state_choice), splitted by ',' | 订单状态集 |
| rb_type    | Integer                           | 回收站类型 |
| lat | Decimal | 当前位置经度 |
| lng | Decimal | 当前位置纬度 |
| page | Integer | 页码 |
| page_per_count | Integer | 每页个数 |

### HTTP应答参数

| 参数名称 | 类型                                                         | 含义     |
| -------- | ------------------------------------------------------------ | -------- |
| orders   | List of {order: [OrderView](/View/order/order/), distance: Float} | 订单列表 |

### 注释

to_grab=true时，返回B端可抢订单列表。

### 请求例

```http
GET /order/b/order/list/?user_sid=d1eb31ca-4aed-11e9-a860-acde48001122&to_grab=true&lat=39.9621301&lng=116.3574610
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "n_pages": 1,
        "result": 200,
        "orders": [
            {
                "order": {
                    "id": 662,
                    "create_time": 1553229343,
                    "grab_time": null,
                    "complete_time": null,
                    "o_state": 0,
                    "amount": "0.000",
                    "c_delivery_info": {
                        "id": 85,
                        "address": "北京市海淀区西土城路10号",
                        "contact": null,
                        "house_number": null,
                        "contact_pn": "13261809966",
                        "lat": "39.9621300",
                        "lng": "116.3574400",
                        "can_resolve_gps": true
                    },
                    "recycling_staff": null,
                    "time_remain": 0,
                    "time_remain_b": 0,
                    "target_time": 1553232943,
                    "order_picking_time": {
                        "start_time": 1553328000,
                        "end_time": 1553335199
                    },
                    "can_cancel_b": false,
                    "budget": 26.086956,
                    "delete_code": 2,
                    "bookkeeping": [],
                    "customer_products": [
                        {
                            "quantity": "30.000000",
                            "p_type": {
                                "id": 5,
                                "t_top_name": "废铁",
                                "in_use": true,
                                "description": ""
                            }
                        }
                    ]
                },
                "distance": 1,
                "aggregates": null
            }
        ]
    },
    "context": null
}
```

### 替换接口

| URL                                 | 端   |
| ----------------------------------- | ---- |
| /order/obtain/order_list/           |      |
| /order/obtain/order_list_b/         |      |
| /order/obtain/order_list_by_date/   |      |
| /order/obtain/order_list_by_type/   |      |
| /order/obtain/order_list_by_state/  |      |
| /order/obtain/order_list_by_filter/ |      |



-------

## 一键下单

### URL

*C端*

POST /order/c/order/

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



__响应__
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

### 接口替换

| URL                             | 端   |
| ------------------------------- | ---- |
| /order/operate/one_click_order/ | C    |

-------

## 抢单

### URL

*B端*

POST /order/b/order/fetch/

### HTTP请求参数

| 参数名称 | 类型            | 含义   |
| -------- | --------------- | ------ |
| oid      | PK of OrderInfo | 订单ID |

### HTTP应答

-

### 请求例

```json
{
  "data": {
    "oid": 633
  }
}
```

### 应答例

```json
{
  "version": "2.0",
  "response": {
    "result": 200
  }
}
```

### 替代接口

| URL                              | 端   |
| -------------------------------- | ---- |
| /order/operate/order_complete_b/ | B    |



-------

## 新建扫码、手动记账订单

### URL

*B端*

POST /order/b/order/

### 请求参数

| 参数名称         | 类型                                                         | 含义         |
| ---------------- | ------------------------------------------------------------ | ------------ |
| bookkeeping_type | [order_bookkeeping_type](/View/order/order/#order_bookkeeping_type) | 订单记账类型 |

### 应答

| 字段名称 | 类型            | 含义   |
| -------- | --------------- | ------ |
| id       | PK of OrderInfo | 订单ID |

### 请求例

```json
{
  "data": {
    "bookkeeping_type": 2
  }
}
```

### 应答例

```json
{
  "response": {
    "id": 16
  }
}
```

-----