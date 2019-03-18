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

-------

## 获取装车单列表

### URL

*B端*

GET /business/b/loading/list/

### 请求参数

| 参数名称     | 类型                | 含义         |
| ------------ | ------------------- | ------------ |
| user_sid     | String              |              |
| agg_op       | String(Optional)    | 聚合方式     |
| lc_state_set | String(Optional)    | 装车单状态集 |
| start_time   | Timestamp(Optional) | 起始创建时间 |
| end_time     | Timestamp(Optional) | 结束创建时间 |
| truck        | String(Optional)    | 车牌号       |
| load_id      | Long(Optional)      | 装车单编号   |

### 应答

| 字段名称            | 类型                                                         | 含义             |
| ------------------- | ------------------------------------------------------------ | ---------------- |
| loading_credentials | List of [LoadingCredentialWithAggregateView](/View/business/loading_credential/#loadingcredentialwithaggregateview) | 装车单及汇总列表 |

### 注释

**agg_op**

| 值             | 含义                                   |
| -------------- | -------------------------------------- |
| subtype_b      | 按2级品类汇总，返回对应B端顶级品类名称 |
| subtype_c      | 按2级品类汇总，返回对应C端顶级品类名称 |
| toptype_b      | 按B端1级品类汇总                       |
| toptype_b_unit | 按B端1级品类及单位汇总                 |
| toptype_c      | 按C端1级品类汇总                       |
| toptype_c_unit | 按C端1级品类及单位汇总                 |
| unit           | 按单位汇总                             |

### 请求例

*获取* **已质检** *的装车单列表，并按* **单位** *进行汇总*

```http
GET /business/b/loading/list/?user_sid=562a73ae-45a0-11e9-86aa-00163e00043c&lc_state_set=checked&agg_op=unit
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "n_pages": 1,
        "loading_credentials": [
            {
                "loading_credential": {
                    "id": 3,
                    "truck": "辽B88888",
                    "lc_state": 8,
                    "rb_type": 1,
                    "created_date": "1544888849"
                },
                "aggregate": {
                    "aggregates": [
                        {
                            "quantity": "24.000000",
                            "price": "35.250",
                            "unit": 1
                        }
                    ],
                    "total_price": "35.250"
                }
            }
        ],
        "result": 200
    },
    "context": null
}
```

------

## 获取装车单详情

### URL

*B端*

GET /business/b/loading/

### 请求参数

| 参数名称 | 类型                    | 含义     |
| -------- | ----------------------- | -------- |
| id       | PK of LoadingCredential | 装车单ID |
| user_sid | String                  |          |

### 应答

| 字段名称           | 类型                                                         | 含义   |
| ------------------ | ------------------------------------------------------------ | ------ |
| loading_credential | [LoadingCredentialView](/View/business/loading_credential/#loadingcredentialview) | 装车单 |

### 请求例

```http
GET /business/b/loading/?user_sid=562a73ae-45a0-11e9-86aa-00163e00043c&id=3
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "result": 200,
        "loading_credential": {
            "id": 3,
            "truck": "辽B88888",
            "lc_state": 8,
            "rb_type": 1,
            "created_date": "1544888849",
            "cred_detail": [
                {
                    "id": 4,
                    "category": {
                        "id": 87,
                        "unit": 1,
                        "t_sub_name": "书本",
                        "in_use": false,
                        "toptype_b": {
                            "id": 8,
                            "t_top_name": "废纸B",
                            "in_use": false,
                            "description": ""
                        }
                    },
                    "quantity": "9.000000",
                    "price": "13.500"
                },
                {
                    "id": 5,
                    "category": {
                        "id": 86,
                        "unit": 1,
                        "t_sub_name": "纸壳通货",
                        "in_use": true,
                        "toptype_b": {
                            "id": 8,
                            "t_top_name": "废纸B",
                            "in_use": false,
                            "description": ""
                        }
                    },
                    "quantity": "15.000000",
                    "price": "21.750"
                }
            ]
        }
    },
    "context": null
}
```

-----

## 获取装车单对应质检单详情

### URL

*B端*

GET /business/b/loading/qc/

### 请求参数

| 参数名称 | 类型                                                         | 含义           |
| -------- | ------------------------------------------------------------ | -------------- |
| id       | PK of LoadingCredential                                      | 装车单ID       |
| qc_type  | [qc_type_choice](/View/qc/qc_credential/#qc_type_choice)     | 质检类型       |
| agg_op   | [AggOperationChoice](/View/qc/aggregate/#aggoperationchoice)(Optional) | 聚合方式(可选) |

### 应答

| 字段名称      | 类型                                                         | 含义   |
| ------------- | ------------------------------------------------------------ | ------ |
| qc_credential | [QCCredentialView](/View/qc/qc_credential/#qccredentialview) | 质检单 |
| aggregate     | [QCDetailAggregateListView](/View/qc/aggregate/#qcdetailaggregatelistview) | 聚合   |

### 请求例

*获取1次质检单详情并按单位汇总*

```http
GET /business/b/loading/qc/?user_sid=562a73ae-45a0-11e9-86aa-00163e00043c&agg_op=unit&id=3&qc_type=0
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "aggregate": {
            "aggregates": [
                {
                    "quantity": "10.000000",
                    "price": "50.000",
                    "unit": 1
                }
            ],
            "total_price": "50.000"
        },
        "result": 200,
        "qc_credential": {
            "id": 118,
            "load_id": 3,
            "number_plate": "辽B88888",
            "created_date": 1550039633,
            "closed_date": 1550039633,
            "qc_state": 2,
            "qc_type": 0,
            "credential_detail": [
                {
                    "id": 103,
                    "category": 2,
                    "category_name": "花料",
                    "category_toptype_name": "杂料",
                    "price": "50.000",
                    "quantity": "10.000000"
                }
            ]
        }
    },
    "context": null
}
```

------

