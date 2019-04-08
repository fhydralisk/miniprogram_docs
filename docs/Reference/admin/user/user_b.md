# B端用户后台管理接口

## 获取列表

### URL

*后台*

GET /adminsys/user/b/list/

### 请求参数

| 参数名称       | 类型             | 含义       |
| -------------- | ---------------- | ---------- |
| user_sid       | String           | 会话       |
| count_per_page | Int(Optional)    | 每页条目数 |
| page           | Int(Optional)    | 页码       |
| extra_filter   | String(Optional) | 过滤器     |

### 应答

| 字段名称         | 类型                                                         | 含义                 |
| ---------------- | ------------------------------------------------------------ | -------------------- |
| count_active     | Int                                                          | 可用用户数量         |
| count_inactive   | Int                                                          | 不可用用户数量       |
| count_all        | Int                                                          | 全部用户数量         |
| recycling_staffs | Flatten List of [RecyclingStaffView](/View/business/recycle_bin/#recyclingstaffview) | 【扁平化】回收员列表 |

### 请求例

*获取用户名或手机号中包含'2'的回收员，每页3个，取第1页*

```http
GET /adminsys/user/b/list/?user_sid=user_sid_admin&count_per_page=3&page=0&extra_filter=2
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "n_pages": 3,
        "count_active": 16,
        "recycling_staffs": [
            {
                "user__pn": "15640852342",
                "user__is_active": false,
                "recycle_bin__loc_desc": "甘井子区大关一街38号sss",
                "is_administrator": false,
                "recycle_bin__rb_name": "华中海底捞",
                "recycle_bin__id": 26,
                "modified_time": "1546794895",
                "rs_name": "高社平",
                "id": 20
            },
            {
                "user__pn": "13804265163",
                "user__is_active": false,
                "recycle_bin__loc_desc": "甘井子区南关岭小学",
                "is_administrator": false,
                "recycle_bin__rb_name": "南关岭小学",
                "recycle_bin__id": 22,
                "modified_time": "1546794895",
                "rs_name": "李俊梅",
                "id": 24
            },
            {
                "user__pn": "13940996041",
                "user__is_active": true,
                "recycle_bin__loc_desc": "甘井子区榆石街与松江路交叉口",
                "is_administrator": true,
                "recycle_bin__rb_name": "美林园",
                "recycle_bin__id": 23,
                "modified_time": "1546794895",
                "rs_name": "王贵珍2",
                "id": 25
            }
        ],
        "result": 200,
        "count_all": 23,
        "count_inactive": 7
    },
    "context": null
}
```

## 获取详情

### URL

*后台*

GET /adminsys/user/b/

### 请求参数

| 参数名称 | 类型                       | 含义     |
| -------- | -------------------------- | -------- |
| user_sid | String                     | 会话     |
| id       | Int (FK of RecyclingStaff) | 回收员ID |

### 应答

| 字段名称        | 类型                                                         | 含义             |
| --------------- | ------------------------------------------------------------ | ---------------- |
| recycling_staff | Flatten [RecyclingStaffView](/View/business/recycle_bin/#recyclingstaffview) | 【扁平化】回收员 |

### 请求例

*获取用户名或手机号中包含'2'的回收员，每页3个，取第1页*

```http
GET /adminsys/user/b/list/?user_sid=user_sid_admin&id=20
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "recycling_staff": {
            "user__pn": "15640852342",
            "user__is_active": false,
            "recycle_bin__loc_desc": "甘井子区大关一街38号sss",
            "is_administrator": false,
            "recycle_bin__rb_name": "华中海底捞",
            "recycle_bin__id": 26,
            "modified_time": "1546794895",
            "rs_name": "高社平",
            "user__last_login": null,
            "id": 20
        },
        "result": 200
    },
    "context": null
}
```

------

## 修改

### URL

*后台*

PUT /adminsys/user/b/

### 请求参数

| 参数名称 | 类型                                                         | 含义       |
| -------- | ------------------------------------------------------------ | ---------- |
| id       | Int (FK of RecyclingStaff)                                   | 回收员ID   |
| update   | Partial [RecyclingStaffView](/View/business/recycle_bin/#recyclingstaffview) | 回收员视图 |

### 应答

无

### 请求例

```http
PUT /adminsys/user/b/?user_sid=1677w51zf8zzq2svpszu2th10b9f23zp HTTP/1.1
Host: -
Content-Type: application/json
cache-control: no-cache
Postman-Token: 09cae47f-6def-4e21-832e-0dd1e1b5ebb5
{
    "data": {
        "id": 25,
        "update": {
            "user__pn": "13940996041",
            "user__is_active": true,
            "user__password": "123456",
            "is_administrator": true,
            "rs_name": "王贵珍2"
        }
    }
}------WebKitFormBoundary7MA4YWxkTrZu0gW--
```

### 注释

修改接口的update内所有字段均为可选，更新方式为增量更新。

例如，update下不含user_password，则不对用户的密码进行更新。

-----

## 新增

### URL

*后台*

POST /adminsys/user/b/

### 请求参数

| 参数名称        | 类型                                                         | 含义       |
| --------------- | ------------------------------------------------------------ | ---------- |
| recycling_staff | Partial [RecyclingStaffView](/View/business/recycle_bin/#recyclingstaffview) | 回收员视图 |

### 应答

| 参数名称 | 类型 | 含义     |
| -------- | ---- | -------- |
| id       | Int  | 回收员ID |

### 请求例

```http
POST /adminsys/user/b/?user_sid=1677w51zf8zzq2svpszu2th10b9f23zp HTTP/1.1
Host: -
Content-Type: application/json
cache-control: no-cache
Postman-Token: 9d5962c6-55e2-497d-879f-7e199034bddc
{
    "data": {
        "recycling_staff": {
            "user__password": "123456",
            "user__pn": "13911111114",
            "recycle_bin_id": 23,
            "rs_name": "Test",
            "is_administrator": false
        }
    }
}------WebKitFormBoundary7MA4YWxkTrZu0gW--
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "result": 200,
        "id": 30
    },
    "context": null
}
```

