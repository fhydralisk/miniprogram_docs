# 登录接口

### URL

GET		/adminsys/login/login/

### 请求参数

| 参数名称 | 类型   | 含义     |
| -------- | ------ | -------- |
| username | String | 用户名   |
| password | String | 登陆密码 |

### 应答

| 参数名称  | 类型   | 含义              |
| --------- | ------ | ----------------- |
| user_sid  | String | session_key(会话) |
| user_info | DICT   | 登录用户的信息    |

### 请求例

```http
GET /adminsys/login/login/?username=wxroot&password=123456
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "user_sid": "35d0v4vm1v49z3wiwkiwakc29iys1s1e",
        "user_info": {
            "internal_name": "wxroot",
            "pn": null
        },
        "result": 200
    },
    "context": null
}
```

