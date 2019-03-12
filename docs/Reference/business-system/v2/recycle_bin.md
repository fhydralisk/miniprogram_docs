# 回收站相关接口

## 获取所在回收站收货价格列表

### URL

*B端*

GET /business/b/rb/product/list/

### 请求参数

user_sid

### 应答

| 字段         | 类型                                                         | 含义     |
| ------------ | ------------------------------------------------------------ | -------- |
| categories   | List of [ProductTopTypeView](/View/category/category/#producttoptypeview) | 种类列表 |
| last_updated | Timestamp                                                    | 时间戳   |

### 请求例

```http
GET /business/b/rb/product/list/?user_sid=tttaaa
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "last_updated": 1545052725,
        "result": 200,
        "categories": [
            {
                "id": 28,
                "t_top_name": "杂料(塑)",
                "in_use": true,
                "product_sub_type": [
                    {
                        "id": 91,
                        "unit": 1,
                        "t_sub_name": "白料",
                        "in_use": true,
                        "price": 1.0
                    },
                    {
                        "id": 92,
                        "unit": 1,
                        "t_sub_name": "花料",
                        "in_use": true,
                        "price": 1.0
                    },
                    {
                        "id": 93,
                        "unit": 1,
                        "t_sub_name": "其他杂料",
                        "in_use": true,
                        "price": 1.0
                    }
                ],
                "description": ""
            },
            {
                "id": 29,
                "t_top_name": "易拉罐B",
                "in_use": true,
                "product_sub_type": [
                    {
                        "id": 94,
                        "unit": 2,
                        "t_sub_name": "易拉罐",
                        "in_use": true,
                        "price": 1.0
                    },
                    {
                        "id": 95,
                        "unit": 1,
                        "t_sub_name": "测试",
                        "in_use": true,
                        "price": 1.0
                    }
                ],
                "description": ""
            }
        ]
    },
    "context": null
}
```

### 接口替换

| URL                                 | 备注 |
| ----------------------------------- | ---- |
| /business/obtain/rb_product_detail/ |      |
|                                     |      |

--------

## 回收站详情

### URL

*C端*

GET /business/c/rb/distance/

### 请求参数

| 参数名称 | 类型          | 含义     |
| -------- | ------------- | -------- |
| user_sid |               |          |
| rb_id    | FK RecycleBin | 回收站ID |
| lat      | Decimal(可选) | 纬度     |
| lng      | Decimal(可选) | 经度     |

### 应答参数

| 字段          | 类型                                                   | 含义         |
| ------------- | ------------------------------------------------------ | ------------ |
| recycle_bin   | [RecycleBin](/Model/business/recycle_bin-model/) Model | 回收站详情   |
| distance      | Float                                                  | 距离（米）   |
| position_desc | Dict                                                   | 地点详细信息 |

### 请求例

```http
GET /business/c/rb/distance/?rb_id=3&user_sid=tttaaa&lat=38.8832&lng=121.3526
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "distance": 36437.0,
        "recycle_bin": {
            "id": 3,
            "GPS_L": "121.6614180",
            "GPS_A": "38.9936400",
            "rb_name": "测试回收站1位于国金大厦11楼103",
            "r_b_type": 1,
            "loc_desc": "测试回收站3",
            "pn": "13472863623",
            "admins": [
                '张三',
            ],
            "c_products": [
                {
                    "id": 19,
                    "t_top_name": "塑料瓶",
                    "in_use": true,
                    "description": "",
                    "price_max": "3.800",
                    "price_min": "3.000"
                },
                {
                    "id": 24,
                    "t_top_name": "其他塑料",
                    "in_use": true,
                    "description": "",
                    "price_max": "1.900",
                    "price_min": "0.800"
                },
                {
                    "id": 23,
                    "t_top_name": "易拉罐(个)",
                    "in_use": true,
                    "description": "",
                    "price_max": "0.080",
                    "price_min": "0.080"
                }
            ]
        },
        "result": 200,
        "position_desc": {
            "formatted_addresses": {
                "rough": "甘井子区大连宝原招待所北(海北路北)",
                "recommend": "甘井子区大连宝原招待所北(海北路北)"
            },
            "address": "辽宁省大连市甘井子区海北路"
        }
    },
    "context": null
}
```

### 替换接口

| URL                         | 备注 |
| --------------------------- | ---- |
| /business/obtain/rb_detail/ |      |
|                             |      |

------

## 获取附近回收站

### URL

*C端*

GET /business/c/rb/distance/list/

### 请求参数

| 参数名称 | 类型    | 说明 |
| -------- | ------- | ---- |
| lat      | Decimal | 纬度 |
| lng      | Decimal | 经度 |

### 应答参数

| 字段    | 类型                                                         | 说明             |
| ------- | ------------------------------------------------------------ | ---------------- |
| closest | List of Dict(<br />  'recycle_bin': [RecycleBin](/Model/business/recycle_bin-model/)<br />  'distance': Float<br />) | 回收站、距离列表 |

### 请求例

```http
GET /business/c/rb/distance/list/?lat=38.8832&lng=121.3526
```



### 应答例

```json
{
    "version": "2.0",
    "response": {
        "result": 200,
        "closest": [
            {
                "recycle_bin": {
                    "id": 8,
                    "GPS_L": "121.5324090",
                    "GPS_A": "38.9626030",
                    "rb_name": "舒雅宾馆",
                    "r_b_type": 0,
                    "loc_desc": "辽宁省大连市甘井子区辛寨子街道辛塔街9号",
                    "pn": "15142487056",
                    "admins": [],
                    "c_products": [
                        {
                            "id": 19,
                            "t_top_name": "塑料瓶",
                            "in_use": true,
                            "description": "",
                            "price_max": "4.100",
                            "price_min": "3.300"
                        },
                        {
                            "id": 24,
                            "t_top_name": "其他塑料",
                            "in_use": true,
                            "description": "",
                            "price_max": "2.200",
                            "price_min": "1.100"
                        },
                        {
                            "id": 23,
                            "t_top_name": "易拉罐(个)",
                            "in_use": true,
                            "description": "",
                            "price_max": "0.100",
                            "price_min": "0.100"
                        },
                    ]
                },
                "distance": 22804.0
            },
            {
                "recycle_bin": {
                    "id": 23,
                    "GPS_L": "121.5545090",
                    "GPS_A": "38.9748440",
                    "rb_name": "美林园",
                    "r_b_type": 0,
                    "loc_desc": "甘井子区榆石街与松江路交叉口",
                    "pn": "13940996041",
                    "admins": [],
                    "c_products": [
                        {
                            "id": 19,
                            "t_top_name": "塑料瓶",
                            "in_use": true,
                            "description": "",
                            "price_max": "4.100",
                            "price_min": "3.300"
                        },
                        {
                            "id": 24,
                            "t_top_name": "其他塑料",
                            "in_use": true,
                            "description": "",
                            "price_max": "2.200",
                            "price_min": "1.100"
                        },
                        {
                            "id": 23,
                            "t_top_name": "易拉罐(个)",
                            "in_use": true,
                            "description": "",
                            "price_max": "0.100",
                            "price_min": "0.100"
                        }
                    ]
                },
                "distance": 25461.0
            }
        ]
    },
    "context": null
}
```

### 注释

接口返回数据量较大，请尽可能缓存。

### 替换接口

| URL                      | 备注 |
| ------------------------ | ---- |
| /business/obtain/nearby/ |      |
|                          |      |