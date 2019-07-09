# 站长后台管理接口

# 获取列表

### URL

后台

GET /adminsys/user/r/list/

### 请求参数

| 参数名称       | 类型             | 含义       |
| -------------- | ---------------- | ---------- |
| user_sid       | String           | 会话       |
| count_per_page | Int(Optional)    | 每页条目数 |
| page           | Int(Optional)    | 页码       |
| extra_filter   | String(Optional) | 过滤器     |

### 应答

| 字段名称       | 类型 | 含义                 |
| -------------- | ---- | -------------------- |
| count_active   | Int  | 可用用户数量         |
| count_inactive | Int  | 不可用用户数量       |
| count_all      | Int  | 全部用户数量         |
| referrers      | List | 【扁平化】推荐人列表 |

### 请求例

获取用户名或手机号中包含'1'的站长,每页3个,取第1页

```http
GET /adminsys/user/r/list/?user_sid=user_sid_admin&count_per_page=3&page=0&extra_filter=1

```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "n_pages": 4,
        "count_active": 10,
        "result": 200,
        "count_all": 10,
        "referrers": [
            {
                "name": "樊1",
                "referrer_code": "aba5a6f5dba0432aaf245b62335651d0",
                "r_state": "pass",
                "expire_date": 1548946500,
                "operator": null,
                "position": null,
                "percentage": "0.0000",
                "pass_date": null,
                "id": 2,
                "user__pn": "18513958704"
            },
            {
                "name": "weqweqw",
                "referrer_code": "8e3d249bddcb42ffa6a415f7ba1fe99e",
                "r_state": "pass",
                "expire_date": 1551323820,
                "operator": null,
                "position": null,
                "percentage": "0.0000",
                "pass_date": null,
                "id": 3,
                "user__pn": "15900659180"
            },
            {
                "name": "崔玉珊",
                "referrer_code": "47af18026c6b4d30bfabdfc33c227cd6",
                "r_state": "pass",
                "expire_date": 1864723920,
                "operator": null,
                "position": null,
                "percentage": "0.0100",
                "pass_date": null,
                "id": 4,
                "user__pn": "13261809966"
            }
        ],
        "count_inactive": 0
    },
    "context": null
}
```

# 获取详情

### URL

后台

GET  /adminsys/user/r/qr/

### 请求参数

| 参数名称 | 类型   | 含义     |
| -------- | ------ | -------- |
| user_sid | String | 会话     |
| id       | Int    | 推荐人ID |

### 应答

| 字段名称 | 类型  | 含义         |
| -------- | ----- | ------------ |
| qr_bin   | image | 推荐人二维码 |

### 请求列

获取用户名或用户手机号中推荐人ID为3的推荐人二维码

```http
GET /adminsys/user/r/qr/?user_sid=user_id_admin&id=3
```

### 应答例

无

# 获取详情

### URL

后台

GET  /adminsys/user/r/

### 请求参数

| 参数名称 | 类型   | 含义     |
| -------- | ------ | -------- |
| user_id  | String | 会话     |
| id       | Int    | 推荐人ID |

### 应答

| 字段名称 | 类型 | 含义       |
| -------- | ---- | ---------- |
| referrer | Dict | 推荐人信息 |

### 请求例

获取推荐人ID为3的推荐人信息

```http
GET /adminsys/user/r/?user_sid=pz23kuvify7z0brahp0ywne61iqinyf3&id=3
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "referrer": {
            "name": "weqweqw",
            "referrer_code": "8e3d249bddcb42ffa6a415f7ba1fe99e",
            "r_state": "pass",
            "expire_date": 1551323899,
            "operator": null,
            "position": "3",
            "percentage": "0.0000",
            "pass_date": null,
            "id": 3,
            "user__pn": "15900659180"
        },
        "result": 200
    },
    "context": null
}
```

------

# 修改

### URL

后台

PUT /adminsys/user/r/

### 请求参数

| 参数名称 | 类型            | 含义       |
| -------- | --------------- | ---------- |
| id       | Int             | 推荐人ID   |
| update   | Partial Flatten | 推荐人视图 |

### 应答

无

### 请求例

```http
PUT /adminsys/user/r/?user_sid=pz23kuvify7z0brahp0ywne61iqinyf3&id=3
Host: -
Content-Type: application/json
cache-control: no-cache
Postman-Token: 7il3l1l3zf-ggas-omah-a08g-xqf70kpo1c
{
	"data":{
		"id":3,
		"update":{
					"name":"weqweqw",
					"percentage":"0.0000",
					"expire_date":1551323899,
					"r_state":"pass",
					"position":"3",
					"operator":"1"
		}
	}
}
```

### 应答例

表示更新成功

{
    "version": "2.0",
    "response": {
        "result": 200
    },
    "context": null
}

### 注释

修改接口的update内所有字段均为可选，更新方式为增量更新。
