# 一对多分享

## 获取分享者的分享码

### URL

/share1vn_event/referrer/

### HTTP请求方式

__GET__

### HTTP请求参数

无（但需要提交user_sid）

### HTTP响应参数

| 参数名称 | 参数类型 | 参数描述 |
| -------- | -------- | -------- |
| code     | String   | 邀请码   |

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
GET /share1vn_event/referrer/?user_sid=f4bd5621-f196-11e8-bb37-6c96cfdf6ce7
```

__响应__

```json
{
    "response": {
        "code": "1x2v3vsa3vadafba9234",
        "result": 200
    }
}
```

## 获取邀请人参加情况

### URL

/share1vn_event/referrer/referee/list/

### HTTP请求方式

__GET__

### HTTP请求参数

| 参数名称  | 参数类型        | 参数描述                                                     |
| --------- | --------------- | ------------------------------------------------------------ |
| is_closed | Boolean（可选） | 可选，True表示用户已经完成第一笔订单，False表示用户尚未完成订单，不传该变量则不做限定。 |

### HTTP响应参数

| 参数名称 | 参数类型 | 参数描述 |
| -------- | -------- | -------- |
| shares     | List   | 受邀请人使用状态 |
| closed_count | Integer | 已完成首投数量 |
| open_count | Integer | 未完成首投数量 |

shares:

| 字段名称           | 字段类型  | 字段描述                                         |
| ------------------ | --------- | ------------------------------------------------ |
| user               | Dict      | {"pn": "电话号码", "name": "用户姓名（若实名）"} |
| first_order_amount | Decimal   | 首投金额                                         |
| promotion          | Decimal   | 获得提成                                         |
| is_closed          | Boolean   | 是否已首投                                       |
| share_date         | Timestamp | 邀请时间                                         |
| closed_date        | Timestamp | 首投时间                                         |

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
GET /share1vn_event/referrer/referee/list/?user_sid=f4bd5621-f196-11e8-bb37-6c96cfdf6ce7
```

__响应__

```json
{
    "response": {
        "open_count": 1,
        "closed_count": 1,
        "shares": [
            {
                "user": {
            		"pn": "138000323000",
            		"name": "王五",
            	},
                "first_order_amount": null,
                "promotion": null,
                "is_closed": false,
                "share_date": 15133239352,
                "closed_date": null,
            },{
                "user": {
            		"pn": "138000324000",
            		"name": "赵六",
            	},
                "first_order_amount": "100.000",
                "promotion": "1.000",
                "is_closed": true,
                "share_date": 15133439352,
                "closed_date": 15133555323,
            }
        ],
        "result": 200
    }
}
```





