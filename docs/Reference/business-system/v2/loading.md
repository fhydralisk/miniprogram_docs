# 装车单相关接口

## 获取待装车订单列表

### URL

*B端*

GET /business/b/loading/preload/list/

### 请求参数

| 参数名称 | 类型 | 含义 |
| -------- | ---- | ---- |
| user_sid |      |      |

### 应答

| 字段名称         | 类型                                                        | 含义                 |
| ---------------- | ----------------------------------------------------------- | -------------------- |
| end_time         | Timestamp                                                   | 上次装车时间         |
| last_until_now   | Long                                                        | 距离上次装车时间秒数 |
| price            | Decimal                                                     | 总金额               |
| quantity_by_unit | [OrderBookkeepingAggregateListView](/View/order/aggregate/) | 按单位汇总           |
| orders           | List of [OrderView](/View/order/order/)                     | 订单列表             |
| aggregates       | [OrderBookkeepingAggregateListView](/View/order/aggregate/) | 按B端品类汇总        |

### 请求例

```http
GET /business/b/loading/preload/list/?user_sid=a1b2c3d4e567
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "result": 200,
        "price": "1.000",
        "quantity_by_unit": {
            "aggregates": [
                {
                    "quantity": "1.000000",
                    "price": "1.000",
                    "unit": 1
                }
            ],
            "total_price": "1.000"
        },
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
                    "sub_type": {
                        "id": 91,
                        "unit": 1,
                        "t_sub_name": "白料"
                    }
                }
            ],
            "total_price": "1.000",
            "total_quantity": "1.000000"
        },
        "orders": [
            {
                "id": 636,
                "complete_time": 1551886890,
                "amount": "1.000",
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
                ]
            }
        ],
        "last_until_now": 490301,
        "end_time": 1551886890
    },
    "context": null
}
```

### 接口替换

本接口替换如下原有接口

| URL                                   | 备注 |
| ------------------------------------- | ---- |
| business/b/truck/obtain_truck_info/   |      |
| business/b/truck/obtain_truck_detail/ |      |