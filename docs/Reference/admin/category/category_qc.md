# 场地端全局品类相关接口(4-3-3)

## 获取场地端全局品类的列表

### URL

```http
GET /adminsys/category/qc/list/
```

### 请求参数

| 参数名称 | 类型 | 含义                   |
| -------- | ---- | ---------------------- |
| id       | Int  | 顶级品类ID(默认为None) |

### 应答

| 参数名称  | 类型 | 含义                     |
| --------- | ---- | ------------------------ |
| sub_types | List | 顶级品类下的二级品类信息 |

### 请求例

获取ID=33的顶级品类下的二级品类信息

```http
GET /adminsys/category/qc/list/?id=33
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "result": 200,
        "sub_types": [
            {
                "id": 30,
                "name": "铝合金",
                "unit": 1,
                "price_default": "1.000",
                "has_tax": true,
                "in_use": true,
                "toptype_id": 33
            },
            {
                "id": 31,
                "name": "断桥铝",
                "unit": 1,
                "price_default": "1.000",
                "has_tax": true,
                "in_use": true,
                "toptype_id": 33
            },
            {
                "id": 32,
                "name": "杂铝",
                "unit": 1,
                "price_default": "1.000",
                "has_tax": true,
                "in_use": true,
                "toptype_id": 33
            },
            {
                "id": 33,
                "name": "件铝",
                "unit": 1,
                "price_default": "1.000",
                "has_tax": true,
                "in_use": true,
                "toptype_id": 33
            },
            {
                "id": 34,
                "name": "白钢(304)",
                "unit": 1,
                "price_default": "1.000",
                "has_tax": true,
                "in_use": true,
                "toptype_id": 33
            },
            {
                "id": 35,
                "name": "白钢(316)",
                "unit": 1,
                "price_default": "1.000",
                "has_tax": true,
                "in_use": true,
                "toptype_id": 33
            },
            {
                "id": 36,
                "name": "白钢(201)",
                "unit": 1,
                "price_default": "1.000",
                "has_tax": true,
                "in_use": true,
                "toptype_id": 33
            },
            {
                "id": 37,
                "name": "白钢(301)",
                "unit": 1,
                "price_default": "1.000",
                "has_tax": true,
                "in_use": true,
                "toptype_id": 33
            },
            {
                "id": 38,
                "name": "白钢(430)",
                "unit": 1,
                "price_default": "1.000",
                "has_tax": true,
                "in_use": true,
                "toptype_id": 33
            },
            {
                "id": 39,
                "name": "红铜",
                "unit": 1,
                "price_default": "1.000",
                "has_tax": true,
                "in_use": true,
                "toptype_id": 33
            },
            {
                "id": 40,
                "name": "黄铜",
                "unit": 1,
                "price_default": "1.000",
                "has_tax": true,
                "in_use": true,
                "toptype_id": 33
            }
        ]
    },
    "context": null
}
```

---

## 场地全局品类的增删改接口

### URL

```http
POST /adminsys/category/qc/
```

### 请求参数

| 参数名称 | 类型 | 含义                 |
| -------- | ---- | -------------------- |
| sub_type | DICT | 要添加的二级品类信息 |

### 应答

无

### 注释

sub_type中必填字段

| 字段名     | 类型    | 含义         |
| ---------- | ------- | ------------ |
| toptype_id | Int     | 顶级品类ID   |
| name       | String  | 二级品类名称 |
| unit       | Int     | 单位         |
| has_tax    | Boolean | 是否含税     |

### 请求例

```http
POST /adminsys/category/qc/?user_sid=s27hk7ox4omne17xiuyg4wvecplz37ae	HTTP 1.1
Host: -
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"sub_type":{
			"toptype_id":33,
			"name":"花岗岩",
			"unit":2,
			"has_tax":"true"
		}
	}
}

```

### 应答例

{
    "version": "2.0",
    "response": {
        "result": 200,
        "id": 48
    },
    "context": null
}

---

### URL

```http
PUT /adminsys/category/qc/
```

### 请求参数

| 参数名称      | 类型    | 含义                       |
| ------------- | ------- | -------------------------- |
| id            | Int     | QC端的商品ID(二级商品的ID) |
| update        | DICT    | 更新的数据信息             |
| refresh_price | Boolean | 是否刷新价格               |

### 应答

无

### 请求例

```http
GET /adminsys/category/qc/?user_sid=s27hk7ox4omne17xiuyg4wvecplz37ae
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"id":48,
		"update":{
				"name":"小红同学"
			},
		"refresh_price":"true"
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

---

### URL

```HTTP
DELETE /adminsys/category/qc/
```

### 请求参数

| 参数名称 | 类型 | 含义       |
| -------- | ---- | ---------- |
| id       | Int  | 二级品类ID |

### 应答

| 参数名称 | 类型    | 含义     |
| -------- | ------- | -------- |
| in_use   | Boolean | 是否在用 |

### 注释

DELETE接口是软删除，通过将正在用的二级品类的in_use修改成False，来代表删除。in_use=False的商品是不进行显示的。

## 场地端全局品类排序

### URL

POST /adminsys/category/qc/ordering/

### 请求参数

| 参数名称 | 类型   | 含义         |
| -------- | ------ | ------------ |
| id       | Int    | 二级品类的ID |
| oo       | Choice | 上移或这下移 |

### 注释

oo

| 值   | 含义 |
| ---- | ---- |
| 1    | 上移 |
| -1   | 下移 |

### 请求例

```http
POST /adminsys/category/qc/ordering/?
user_sid=8p2r7n015e8y2i1awjdsylmw89uuot4o
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"id":47,
		"oo":1
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