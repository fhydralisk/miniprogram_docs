# 展示用订单-站长接口

## 订单-站长接口

### URL

GET /order/refer/order_list/

### 请求参数

| 参数名称       | 类型                | 含义                            |
| -------------- | ------------------- | ------------------------------- |
| start_time     | Timestamp(Optional) | 订单起始时间戳(可选过滤条件)    |
| end_time       | Timestamp(Optional) | 订单截止时间戳(可选过滤条件)    |
| no_refer       | Boolean(Optional)   | 无站长(可选过滤条件)            |
| page           | Integer             | 页码(从0开始)                   |
| page_per_count | Integer             | 每页数量                        |
| user_sid       | String              | 用户会话ID(需登录B端的用户会话) |

### 应答

| 字段名称 | 类型                          | 含义          |
| -------- | ----------------------------- | ------------- |
| orders   | List of OrderWithReferrerView | 站长-订单视图 |
| n_pages  | Integer                       | 总页数        |

**OrderWithReferrerView**

| 字段名称      | 类型      | 含义       |
| ------------- | --------- | ---------- |
| amount        | Decimal   | 订单金额   |
| rs_name       | String    | 回收员姓名 |
| client_pn     | String    | 客户手机号 |
| promotion     | Decimal   | 提成金额   |
| referrer_name | String    | 站长姓名   |
| complete_time | Timestamp | 完成时间   |

### 请求例

获取有站长的订单列表，每页3个，返回第一页。

```http
GET /order/refer/order_list/?page=0&page_per_count=3&no_refer=false&user_sid=000-111-sss-3333
```

### 应答例

```json
{
    "version": "0.1",
    "response": {
        "n_pages": 17,
        "result": 200,
        "orders": [
            {
                "amount": 365.9,
                "rs_name": "张健",
                "client_pn": "13942673871",
                "promotion": 7.318,
                "referrer_name": "崔峻嘉",
                "complete_time": 1553755131
            },
            {
                "amount": 1411.2,
                "rs_name": "李强",
                "client_pn": "15942872728",
                "promotion": 28.224,
                "referrer_name": "程谋林",
                "complete_time": 1553752756
            },
            {
                "amount": 545.3,
                "rs_name": "张健",
                "client_pn": "13591114473",
                "promotion": 10.906,
                "referrer_name": "崔峻嘉",
                "complete_time": 1553671876
            }
        ]
    },
    "context": null
}
```

