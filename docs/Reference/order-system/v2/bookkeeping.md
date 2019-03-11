# 记账相关接口

## 记账汇总（聚合）接口

获取用户已完成订单B端记账单的分类汇总

### URL

*C端*

GET /order/c/order/bookkeeping/aggregate/group/

*B端*

GET /order/b/order/bookkeeping/aggregate/group/

### 请求参数

| 参数名称 | 类型   | 含义     |
| -------- | ------ | -------- |
| agg_op   | String | 汇总方式 |
| user_sid |        |          |

### 应答

| 字段名称 | 类型                                                        | 含义           |
| -------- | ----------------------------------------------------------- | -------------- |
| all      | [OrderBookkeepingAggregateListView](/View/order/aggregate/) | 全部记账单汇总 |
| loaded   | [OrderBookkeepingAggregateListView](/View/order/aggregate/) | 装车记账单汇总 |
| month    | [OrderBookkeepingAggregateListView](/View/order/aggregate/) | 月汇总         |
| week     | [OrderBookkeepingAggregateListView](/View/order/aggregate/) | 周汇总         |
| day      | [OrderBookkeepingAggregateListView](/View/order/aggregate/) | 日汇总         |

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
GET /order/b/order/bookkeeping/aggregate/group/?user_sid=tttaaa&agg_op=toptype_b_unit
```

### 应答示例

```json
{
    "version": "2.0",
    "response": {
        "week": {
            "aggregates": [],
            "total_price": "0.000"
        },
        "all": {
            "aggregates": [
                {
                    "quantity": "27.100000",
                    "price": "27.100",
                    "top_type": {
                        "id": 28,
                        "t_top_name": "杂料(塑)",
                        "in_use": true
                    },
                    "unit": 1
                },
                {
                    "quantity": "1.000000",
                    "price": "1.000",
                    "top_type": {
                        "id": 31,
                        "t_top_name": "玻璃类B",
                        "in_use": true
                    },
                    "unit": 1
                },
                {
                    "quantity": "1.000000",
                    "price": "1.000",
                    "top_type": {
                        "id": 29,
                        "t_top_name": "易拉罐B",
                        "in_use": true
                    },
                    "unit": 2
                }
            ],
            "total_price": "29.100"
        },
        "loaded": {
            "aggregates": [
                {
                    "quantity": "27.100000",
                    "price": "27.100",
                    "top_type": {
                        "id": 28,
                        "t_top_name": "杂料(塑)",
                        "in_use": true
                    },
                    "unit": 1
                },
                {
                    "quantity": "1.000000",
                    "price": "1.000",
                    "top_type": {
                        "id": 31,
                        "t_top_name": "玻璃类B",
                        "in_use": true
                    },
                    "unit": 1
                },
                {
                    "quantity": "1.000000",
                    "price": "1.000",
                    "top_type": {
                        "id": 29,
                        "t_top_name": "易拉罐B",
                        "in_use": true
                    },
                    "unit": 2
                }
            ],
            "total_price": "29.100"
        },
        "day": {
            "aggregates": [],
            "total_price": "0.000"
        },
        "month": {
            "aggregates": [
                {
                    "quantity": "22.100000",
                    "price": "22.100",
                    "top_type": {
                        "id": 28,
                        "t_top_name": "杂料(塑)",
                        "in_use": true
                    },
                    "unit": 1
                },
                {
                    "quantity": "1.000000",
                    "price": "1.000",
                    "top_type": {
                        "id": 31,
                        "t_top_name": "玻璃类B",
                        "in_use": true
                    },
                    "unit": 1
                },
                {
                    "quantity": "1.000000",
                    "price": "1.000",
                    "top_type": {
                        "id": 29,
                        "t_top_name": "易拉罐B",
                        "in_use": true
                    },
                    "unit": 2
                }
            ],
            "total_price": "24.100"
        },
        "result": 200,
    },
    "context": null
}
```

### 接口替换

本接口替换如下原有接口

| URL                             | 备注 |
| ------------------------------- | ---- |
| /order/c/detail/summary/        |      |
| /order/obtain/order_list_count/ |      |

---------

