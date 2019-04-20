# 用户校验相关的接口

## 获取用户认证详情

### URL

GET	/adminsys/validate/

### 请求参数

| 参数名称 | 类型   | 含义   |
| -------- | ------ | ------ |
| user_sid | String | 会话   |
| id       | Int    | 用户ID |

### 应答

| 参数名称      | 类型 | 含义               |
| ------------- | ---- | ------------------ |
| user_validate | DICT | 【扁平化】用户信息 |

### 请求例

获取用户id为1 的用户信息

```http
GET /adminsys/validate/?id=1
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "user_validate": {
            "name": "孙悟空",
            "idcard_number": "22222222222222",
            "user__internal_name": "oA8H64ugV3Tr_dXgBhN77PeTwlI4",
            "validate_status": "accepted",
            "uid": 7,
            "id": 1,
            "user__pn": "13717611792"
        },
        "result": 200
    },
    "context": null
}
```

## 审核通过/拒绝用户的接口

### URL

POST	/adminsys/validate/operate/

### 请求参数

| 参数名称        | 类型   | 含义       |
| --------------- | ------ | ---------- |
| user_sid        | String | 会话       |
| id              | Int    | 用户ID     |
| validate_status | Alias  | 校验的状态 |

### 应答

wu

### 注释

validate_status

| 值       | 含义                                 |
| -------- | ------------------------------------ |
| accepted | 用户已提交认证审核申请，且审核已通过 |
| rejected | 用户已提交认证审核申请，审核被拒绝   |

### 请求例

```http
POST	/adminsys/validate/operate/  HTTP/1.1
Host: -
Content-Type: applicate/json
Postman-Token:hkwm3819jtkx6tqqc8unyfaeeb20ji8j
{
	"data":{
		"id":1,
		"validate_status":"rejected"
	}
}

```

### 应答例

{
    "version": "2.0",
    "response": {
        "result": 200
    },
    "context": null
}

## 获取用户认证列表

### URL

GET	/adminsys/validate/list/

### 请求参数

| 参数名称        | 类型                | 含义       |
| --------------- | ------------------- | ---------- |
| user_sid        | String              | 会话       |
| validate_status | Alias(Optional)     | 校验的状态 |
| submit_date     | Timestamp(Optional) | 提交时间   |
| page            | Int(Optional)       | 页码       |
| count_per_page  | Int(Optional)       | 每页条目数 |
| extra_filter    | String(Optional)    | 过滤器     |

### 应答

| 参数名称            | 类型 | 含义                   |
| ------------------- | ---- | ---------------------- |
| count_all           | Int  | 总人数                 |
| count_need_validate | Int  | 需要验证的人数         |
| user_validate       | List | 验证通过的用户信息列表 |
| n_pages             | Int  | 页码数                 |

### 注释

validate_status

| 值       | 含义       |
| -------- | ---------- |
| accepted | 审核通过   |
| rejected | 审核被拒绝 |

### 请求例

获取用户认证列表中状态为rejected的用户信息

```http
GET /adminsys/validate/list/?validate_status=rejected
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "n_pages": 1,
        "count_all": 1,
        "result": 200,
        "count_need_validate": 0,
        "user_validates": [
            {
                "passed_date": 1555347835,
                "name": "孙悟空",
                "submit_date": null,
                "idcard_number": "22222222222222",
                "user__internal_name": "oA8H64ugV3Tr_dXgBhN77PeTwlI4",
                "validate_status": "rejected",
                "uid": 7,
                "id": 1,
                "user__pn": "13717611792"
            }
        ]
    },
    "context": null
}
```

## 获取用户认证照片

### URL

GET	/adminsys/validate/photo/

### 请求参数

| 参数名称 | 类型  | 含义     |
| -------- | ----- | -------- |
| user_sid | Int   | 会话     |
| id       | Int   | 用户ID   |
| t_photo  | Alias | 照片类型 |

### 应答

| 参数名称             | 类型       | 含义                |
| -------------------- | ---------- | ------------------- |
| FileResponse         | image      | 验证通过的用户照片  |
| HttpResponseNotFound | text/plain | 抛异常，photo不存在 |

### 注释

t_photo

| 值      | 含义           |
| ------- | -------------- |
| handled | 手持证件的照片 |
| top     | 身份证正面照   |
| bottom  | 身份证反面照   |



如果存在，就返回用户验证通过的照片

否则，会提示用户photo不存在

### 请求例

获取用户ID为1的用户，手持身份证的照片

```http
GET /adminsys/validate/photo/?id=1&t_photo=handled
```

### 应答例

暂无数据

如果没有数据，应答如下

Photo does not exist

