# C端用户后台管理接口

## 获取C端用户信息列表

### URL

后台

GET  /adminsys/user/c/list/

### 请求参数

| 参数名称        | 类型             | 含义       |
| --------------- | ---------------- | ---------- |
| user_sid        | String           | 会话       |
| counte_per_page | Int(Optional)    | 每页条目数 |
| page            | Int(Optional)    | 页码       |
| extra_filter    | String(Optional) | 过滤器     |

### 应答

| 字段名称       | 类型 | 含义               |
| -------------- | ---- | ------------------ |
| users          | List | C端用户信息        |
| n_page         | Int  | 页码数             |
| count_active   | Int  | 正在使用的用户数量 |
| count_inactive | Int  | 没有再用的用户数量 |
| count_all      | Int  | 总的用户数量       |

### 请求例

获取C端用户，每页3个，取第1页

```http
GET /adminsys/user/c/list/?page=0&count_per_page=3
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "n_pages": 12,
        "count_active": 34,
        "result": 200,
        "count_all": 34,
        "users": [
            {
                "openid": "oA8H64nGBYdDPIaL4Er3JknqddmM",
                "user__pn": "15652933853",
                "nickname": "oA8H64nGBYdDPIaL4Er3JknqddmM",
                "user__is_active": true,
                "user__last_login": 1555505026,
                "user__user_validate": null
            },
            {
                "openid": "oA8H64kyiOeJA-tLefGf2f4IS8Pk",
                "user__pn": "13472863621",
                "nickname": "oA8H64kyiOeJA-tLefGf2f4IS8Pk",
                "user__is_active": true,
                "user__last_login": null,
                "user__user_validate": null
            },
            {
                "openid": "oA8H64vqZyymJIw3LOmK5iwl9cyw",
                "user__pn": null,
                "nickname": "oA8H64vqZyymJIw3LOmK5iwl9cyw",
                "user__is_active": true,
                "user__last_login": null,
                "user__user_validate": null
            }
        ],
        "count_inactive": 0
    },
    "context": null
}
```

