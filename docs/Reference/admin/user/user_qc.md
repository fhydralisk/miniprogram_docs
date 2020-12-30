# QC端用户后台管理接口

# 获取列表

### URL

后台

GET  /adminsys/user/qc/list/

### 请求参数

| 参数名称        | 类型             | 含义       |
| --------------- | ---------------- | ---------- |
| user_id         | String           | 会话       |
| counte_per_page | Int(Optional)    | 每页条目数 |
| page            | Int(Optional)    | 页码       |
| extra_filter    | String(Optional) | 过滤器     |

### 应答

| 字段名称       | 类型    | 含义                 |
| -------------- | ------- | -------------------- |
| count_active   | Int     | 可用用户数量         |
| count_inactive | Int     | 不可用用户数量       |
| count_all      | Int     | 全部用户数量         |
| qc_staffs      | Flatten | 【扁平化】质检员列表 |

### 请求例

获取用户名或手机号中包含"1"的质检员，每页3个，取第1页

```http
GET /adminsys/user/qc/list/?user_sid=pz23kuvify7z0brahp0ywne61iqinyf3&page=0&count_per_page=3&extra_filter=1
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "n_pages": 2,
        "count_active": 6,
        "qc_staffs": [
            {
                "name": "fanhangyu",
                "qc_role": "reviewer",
                "user__is_active": true,
                "qc_place__name": "测试场地2",
                "qc_place__id": 1,
                "join_date": 1548064560,
                "id": 1,
                "qc_place__loc_desc": "不知道aaa",
                "user__pn": "18513958704"
            },
            {
                "name": "测试员1",
                "qc_role": "reviewer",
                "user__is_active": true,
                "qc_place__name": "测试场地2",
                "qc_place__id": 1,
                "join_date": 1550032656,
                "id": 2,
                "qc_place__loc_desc": "不知道aaa",
                "user__pn": "13888888888"
            },
            {
                "name": "测试员222",
                "qc_role": "reviewer",
                "user__is_active": true,
                "qc_place__name": "测试场地2",
                "qc_place__id": 1,
                "join_date": 1550032674,
                "id": 3,
                "qc_place__loc_desc": "不知道aaa",
                "user__pn": "13888888887"
            }
        ],
        "result": 200,
        "count_all": 6,
        "count_inactive": 0
    },
    "context": null
}
```

# 获取详情

### URL

后台

GET  /adminsys/user/qc/

### 请求参数

| 参数名称 | 类型   | 含义     |
| -------- | ------ | -------- |
| user_id  | String | 会话     |
| id       | Int    | 质检员ID |

### 应答

| 字段名称 | 类型    | 含义                 |
| -------- | ------- | -------------------- |
| qc_staff | Flatten | 【扁平化】质检员信息 |

### 请求例

获取ID为1的已登录的质检员

```http
GET /adminsys/user/qc/?user_sid=pz23kuvify7z0brahp0ywne61iqinyf3&id=1
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "qc_staff": {
            "name": "fanhangyu",
            "qc_role": "reviewer",
            "user__is_active": true,
            "qc_place__name": "测试场地2",
            "qc_place__id": 1,
            "join_date": 1548064560,
            "id": 1,
            "qc_place__loc_desc": "不知道aaa",
            "user__pn": "18513958704"
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

PUT  /adminsys/user/qc/

### 请求参数

| 参数名称 | 类型            | 含义     |
| -------- | --------------- | -------- |
| id       | Int             | 质检员ID |
| update   | Partial Flatten | 质检员   |

### 应答

无

### 请求例

```http
PUT /adminsys/user/qc/?user_sid=pz23kuvify7z0brahp0ywne61iqinyf3&id=1
Host: -
Content-Type: application/json
cache-control: no-cache
Postman-Token: 7il3l1l3-zfgg-asom-aha0-8gxqf70kpo1c
{
	"data":{
		"id":1,
		"update":{
					"name":"fanhangyu",
					"qc_role": "reviewer",
            		"user__is_active": true,
		            "qc_place__name": "测试场地3",
		            "qc_place_id": 1,
		            "id":1,
		            "join_date": 1548064560,
		            "qc_place__loc_desc": "不知道ddd",
		            "user__pn": "18513958704"
		}
	}
}

```

### 注释

修改接口的update内所有字段均为可选，更新方式为增量更新。

例如，update下不含user_pn，则不对质检员手机号进行更新。

------

# 新增

### URL

后台

POST  /adminsys/user/qc/

### 请求参数

| 参数名称 | 类型    | 含义       |
| -------- | ------- | ---------- |
| qc_staff | Flatten | 质检员视图 |

### 应答

| 字段名称 | 类型 | 含义     |
| -------- | ---- | -------- |
| id       | Int  | 质检员ID |

### 请求例

```http
POST /adminsys/user/qc/?user_sid=pz23kuvify7z0brahp0ywne61iqinyf3
Host: -
Content-Type: application/json
cache-control: no-cache
Postman-Token: 7il3l1l3-zfgg-asom-aha0-8gxqf70kpo1c
{
	"data":{
		"qc_staff":{
					"name":"fanhangyu",
					"qc_role": "reviewer",
            		"user__is_active": true,
		            "qc_place__name": "测试场地2",
		            "qc_place_id": 1,
		            "id":1,
		            "join_date": 1548064560,
		            "qc_place__loc_desc": "不知道ddd",
		            "user__pn": "18513958705"
		}
	}
}
```

### 应答例

{
    "version": "2.0",
    "response": {
        "result": 200,
        "id": 7
    },
    "context": null
}

