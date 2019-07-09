# B端回收站点管理（4-2-1）

## 获取回收站列表

### URL

```http
GET /adminsys/recycle_bin/list/
```

### 请求参数

| 参数名称       | 类型        | 含义                   |
| -------------- | ----------- | ---------------------- |
| user_sid       | String      | 会话                   |
| r_b_type       | AliasChoice | 回收站类型(默认为None) |
| page           | Int         | 页码(过滤器)           |
| count_per_page | Int         | 每页条目数(过滤器)     |
| extra_filter   | String      | 过滤条件(过滤器)       |

### 应答

| 参数名称    | 类型 | 含义                 |
| ----------- | ---- | -------------------- |
| n_page      | Int  | 当前回收站列表总页数 |
| count_fix   | Int  | 固定站数量           |
| count_flow  | Int  | 流动站站数量         |
| count_all   | Int  | 回收站总数量         |
| recycle_bin | DICT | 回收站的详情         |

### 请求例

```http
GET /adminsys/recycle_bin/list/
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "n_pages": 10,
        "count_fix": 18,
        "count_flow": 10,
        "result": 200,
        "count_all": 28,
        "recycle_bins": [
            {
                "GPS_A": "52.2300000",
                "in_use": true,
                "GPS_L": "20.2491700",
                "loc_desc": "测试回收站1",
                "rb_name": "测试回收站1位于国金大厦11楼101",
                "admins": [],
                "r_b_type": "fix",
                "position_desc": null,
                "pn": "13472863621",
                "id": 1
            },
            {
                "GPS_A": "131.2391100",
                "in_use": true,
                "GPS_L": "121.5082800",
                "loc_desc": "测试回收站2",
                "rb_name": "测试回收站1位于国金大厦11楼102",
                "admins": [],
                "r_b_type": "fix",
                "position_desc": null,
                "pn": "13472863622",
                "id": 2
            },
            {
                "GPS_A": "38.9936400",
                "in_use": true,
                "GPS_L": "121.6614180",
                "loc_desc": "测试回收站3",
                "rb_name": "测试回收站1位于国金大厦11楼103",
                "admins": [],
                "r_b_type": "flow",
                "position_desc": null,
                "pn": "13472863623",
                "id": 3
            }
        ]
    },
    "context": null
}
```

## 获取回收站的简化列表

### URL

```http
GET /adminsys/recycle_bin/simplified/list/
```

### 请求参数

| 参数名称       | 类型        | 含义                   |
| -------------- | ----------- | ---------------------- |
| user_sid       | String      | 会话                   |
| r_b_type       | AliasChoice | 回收站类型(默认为None) |
| page           | Int         | 页码(过滤器)           |
| count_per_page | Int         | 每页条目数(过滤器)     |
| extra_filter   | String      | 过滤条件(过滤器)       |

### 应答

| 参数名称    | 类型 | 含义                 |
| ----------- | ---- | -------------------- |
| n_page      | Int  | 当前回收站列表总页数 |
| count_fix   | Int  | 固定站数量           |
| count_flow  | Int  | 流动站站数量         |
| count_all   | Int  | 回收站总数量         |
| recycle_bin | DICT | 回收站的详情         |

### 请求例

```http
GET /adminsys/recycle_bin/simplified/list/
```

### 应答例

```json
"n_pages": 3,
        "count_fix": 18,
        "count_flow": 10,
        "result": 200,
        "count_all": 28,
        "recycle_bins": [
            {
                "id": 1,
                "rb_name": "测试回收站1位于国金大厦11楼101",
                "r_b_type": "fix"
            },
            {
                "id": 2,
                "rb_name": "测试回收站1位于国金大厦11楼102",
                "r_b_type": "fix"
            },
            {
                "id": 3,
                "rb_name": "测试回收站1位于国金大厦11楼103",
                "r_b_type": "flow"
            },
            {
                "id": 4,
                "rb_name": "测试站点1",
                "r_b_type": "flow"
            },
            {
                "id": 5,
                "rb_name": "华能联合大厦",
                "r_b_type": "fix"
            },
            {
                "id": 6,
                "rb_name": "陆家嘴正大广场",
                "r_b_type": "fix"
            },
            {
                "id": 7,
                "rb_name": "陆家嘴东方明珠电视塔",
                "r_b_type": "fix"
            },
            {
                "id": 8,
                "rb_name": "舒雅宾馆",
                "r_b_type": "fix"
            },
            {
                "id": 9,
                "rb_name": "测试地点1",
                "r_b_type": "flow"
            },
            {
                "id": 10,
                "rb_name": "测试地点2",
                "r_b_type": "fix"
            }
        ]
    },
    "context": null
}
```

## 回收站详情

### URL

```http
GET /adminsys/recycle_bin/
```

### 请求参数

| 参数名称 | 类型 | 含义       |
| -------- | ---- | ---------- |
| id       | Int  | 回收站名称 |

### 应答

| 参数名称    | 类型 | 含义           |
| ----------- | ---- | -------------- |
| recycle_bin | DICT | 回收站详情信息 |

### 请求例

```http
GET /adminsys/recycle_bin/?id=29
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "recycle_bin": {
            "id": 29,
            "GPS_L": null,
            "GPS_A": null,
            "rb_name": "天线宝宝回收",
            "r_b_type": "flow",
            "loc_desc": "保护环境，人人有责",
            "position_desc": null,
            "pn": "8008208821",
            "in_use": true,
            "admins": [],
            "c_products": [],
            "b_products": []
        },
        "result": 200
    },
    "context": null
}
```

---

### URL

```http
POST /adminsys/recycle_bin/
```

### 请求参数

| 参数名称        | 类型    | 含义                        |
| --------------- | ------- | --------------------------- |
| default_product | Boolean | 是否使用默认商品(默认False) |
| recycle_bin     | DICT    | 要增加回收站的信息          |

### 应答

| 参数名称 | 类型 | 含义             |
| -------- | ---- | ---------------- |
| id       | Int  | 增加的回收站的ID |

### 请求例

```http
POST /adminsys/recycle_bin/?user_sid=t4dzib2hcfimmksv3m6nuyu87u5g82jv
Host: -
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"recycle_bin":{
			"rb_name":"天线宝宝回收站",
			"loc_desc":"保护环境，人人有责",
			"r_b_type":"fix",
			"pn":8008208821
		}
	}
}
```

### 应答例

{
    "version": "2.0",
    "response": {
        "result": 200,
        "id": 30
    },
    "context": null
}

---

### URL

```http
PUT /adminsys/recycle_bin/
```

### 请求参数

| 参数名称 | 类型 | 含义                 |
| -------- | ---- | -------------------- |
| id       | Int  | 要修改的回收站的ID   |
| update   | DICT | 要修改的回收站的信息 |

### 应答

无

### 请求例

```http
PUT /adminsys/recycle_bin/?user_sid=t4dzib2hcfimmksv3m6nuyu87u5g82jv
Host: -
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"id":29,
		"update":{
			"rb_name":"天线宝宝回收111",
			"loc_desc":"保护环境，人人有责",
			"r_b_type":"flow",
			"pn":8008208821
		}
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

### 注释

修改接口的update内所有字段均为可选，更新方式为增量更新。