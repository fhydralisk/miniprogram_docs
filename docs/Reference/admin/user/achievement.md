# 站长业绩相关接口（2-2）

## 获取站长绩效列表(2-2-1)

### URL

GET	/adminsys/achievement/achievement/list/

### 请求参数

| 参数名称       | 类型   | 含义       |
| -------------- | ------ | ---------- |
| user_sid       | String | 会话       |
| page           | Int    | 页码       |
| count_per_page | Int    | 每页条目数 |
| extra_filter   | String | 过滤器     |

### 应答

| 参数名称  | 类型 | 含义         |
| --------- | ---- | ------------ |
| referrers | List | 站长绩效信息 |

### 请求例

获取所有站长的站长绩效列表

```http
GET /adminsys/achievement/achievement/list/?user_sid=8p2r7n015e8y2i1awjdsylmw89uuot4o
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "referrers": [
            {
                "user__pn": "18513958704",
                "total_promotion": "20.000",
                "name": "樊1",
                "count_orders": 1,
                "user__internal_name": "18513958704",
                "r_state": "pass",
                "count_users": 0,
                "id": 2,
                "total_amount": "1000.000"
            },
            {
                "user__pn": "15900659180",
                "total_promotion": "0.000",
                "name": "weqweqw",
                "count_orders": 0,
                "user__internal_name": "oA8H64vA1QfwojWo3tlfEWJ1-AHg",
                "r_state": "stop",
                "count_users": 0,
                "id": 3,
                "total_amount": "0.000"
            },
            {
                "user__pn": "13261809966",
                "total_promotion": "2.201",
                "name": "崔玉珊",
                "count_orders": 16,
                "user__internal_name": "oA8H64q3DC_JDMlIwlrjasZBzwAk",
                "r_state": "pass",
                "count_users": 3,
                "id": 4,
                "total_amount": "220.100"
            },
            {
                "user__pn": "15652933853",
                "total_promotion": "0.000",
                "name": "吴敏",
                "count_orders": 0,
                "user__internal_name": "oA8H64nGBYdDPIaL4Er3JknqddmM",
                "r_state": "pass",
                "count_users": 0,
                "id": 5,
                "total_amount": "0.000"
            },
            {
                "user__pn": "15901712060",
                "total_promotion": "0.000",
                "name": "啊啊啊",
                "count_orders": 0,
                "user__internal_name": "oA8H64sErfLD9xcy7ysLPanPOeck",
                "r_state": "pass",
                "count_users": 0,
                "id": 8,
                "total_amount": "0.000"
            },
            {
                "user__pn": "18513958704",
                "total_promotion": "0.000",
                "name": "樊航宇",
                "count_orders": 0,
                "user__internal_name": "oA8H64tWjb8KaBBfQLiJs2c3eq38",
                "r_state": "pass",
                "count_users": 0,
                "id": 9,
                "total_amount": "0.000"
            },
            {
                "user__pn": "13232762061",
                "total_promotion": "0.000",
                "name": "朱老师",
                "count_orders": 0,
                "user__internal_name": "oA8H64mhneVpMCcwNIKngcZv5ObY",
                "r_state": "pass",
                "count_users": 1,
                "id": 10,
                "total_amount": "0.000"
            },
            {
                "user__pn": "17600484487",
                "total_promotion": "0.000",
                "name": "吴姬民",
                "count_orders": 0,
                "user__internal_name": "oA8H64qAYCM_1i4-wC-kD1FLBPBk",
                "r_state": "pass",
                "count_users": 0,
                "id": 11,
                "total_amount": "0.000"
            },
            {
                "user__pn": "15530106031",
                "total_promotion": "0.000",
                "name": "测试1",
                "count_orders": 0,
                "user__internal_name": "oA8H64sVm0IGhqX1pMkUeO80sKwI",
                "r_state": "pass",
                "count_users": 0,
                "id": 12,
                "total_amount": "0.000"
            }
        ],
        "result": 200
    },
    "context": null
}
```

### 获取指定站长提成订单列表

### URL

GET	/adminsys/achievement/order/list/

### 请求参数

| 参数名称        | 类型                | 含义                                     |
| --------------- | ------------------- | ---------------------------------------- |
| id              | Int                 | 站长ID                                   |
| oeder_id        | Int(Optional)       | 订单ID                                   |
| start_time      | Timestamp(Optional) | 起始时间(过滤器)                         |
| end_time        | Timestamp(Optional) | 截止时间(过滤器)                         |
| contact         | String(Optional)    | 联系人新姓名或电话(过滤器)               |
| recycling_staff | String(Optional)    | 回收人员(默认为None)                     |
| include_deleted | Boolean(Optional)   | 是否包括已经删除的订单(过滤器,默认False) |
| r_b_type        | Alias               | 回收站类型                               |
| dispatch_filter | Choice              | 调度的过滤器                             |
| page            | Int(Optional)       | 页码                                     |
| count_per_page  | Int(Optional)       | 每页条目数                               |

### 应答

| 参数名称            | 类型 | 含义               |
| ------------------- | ---- | ------------------ |
| referrer            | DICT | 站长信息           |
| count_flow          | Int  | 流动站订单数量     |
| count_fixed         | Int  | 固定站订单数量     |
| count_all           | Int  | 全部订单数量       |
| count_all_dispatch  | Int  | 被调度的订单数量   |
| count_need_dispatch | Int  | 需要调度的订单数量 |
| n_page              | Int  | 页码数             |
| orders              | List | 订单详情           |

### 请求例

获取站长ID为2的站长订单详情

```http
GET /adminsys/achievement/order/list/?id=2
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "count_all_dispatch": 74,
        "count_fixed": 44,
        "referrer": {
            "name": "樊1",
            "r_state": "pass",
            "id": 2,
            "user__internal_name": "18513958704",
            "user__pn": "18513958704"
        },
        "count_need_dispatch": 2,
        "n_pages": 1,
        "count_flow": 212,
        "result": 200,
        "count_all": 324,
        "orders": [
            {
                "recycling_staff__rs_name": "Test",
                "recycling_staff__rs_pn": "18627661345",
                "o_state": "completed",
                "budget": null,
                "time_remain": 0,
                "client": null,
                "create_time": 1553652956,
                "dispatch_state": "completed",
                "id": 688
            }
        ]
    },
    "context": null
}
```