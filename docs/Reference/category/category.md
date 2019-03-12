# 品类-种类相关接口

## 获取品类及缺省价格区间接口

### URL

*全局*

GET /category/price/

### 请求参数

| 参数名称   | 参数类型 | 含义         |
| ---------- | -------- | ------------ |
| price_type | String   | 区间价格种类 |
| operator   | Int      | 端种类       |

### 应答

| 字段         | 类型                                                         | 含义         |
| ------------ | ------------------------------------------------------------ | ------------ |
| categories   | List of [ProductTopTypeView](/View/category/category/#producttoptype) |              |
| last_updated | Timestamp                                                    | 最后更新时间 |

### 注释

*price_type*

| 值   | 含义   |
| ---- | ------ |
| fix  | 固定站 |
| flow | 流动站 |

*operator*

| 值   | 含义 |
| ---- | ---- |
| 0    | C端  |
| 1    | B端  |

### 请求例

```http
GET /category/price/?price_type=fix&operator=1
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "last_updated": 1552312816,
        "result": 200,
        "categories": [
            {
                "id": 14,
                "t_top_name": "有色金属",
                "in_use": true,
                "product_sub_type": [
                    {
                        "id": 9,
                        "unit": 1,
                        "t_sub_name": "白钢",
                        "in_use": true,
                        "price_default_flow": "20.000",
                        "price_default_fix": "18.000"
                    },
                    {
                        "id": 10,
                        "unit": 1,
                        "t_sub_name": "铜",
                        "in_use": true,
                        "price_default_flow": "30.000",
                        "price_default_fix": "28.000"
                    }
                ],
                "description": "",
                "price": "23.000",
                "price_max": "28.000",
                "price_min": "18.000"
            }
        ]
    },
    "context": null
}
```

### 替换接口

此接口无需替换，但接口返回格式和请求参数有变动

----

