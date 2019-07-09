# 品类-相关的接口文档

# 获取C端/B端顶级品类的列表

### URL

GET /adminsys/category/l1/list/

### 请求参数

| 参数名称 | 参数类型 | 含义   |
| -------- | -------- | ------ |
| optrator | Int      | 端种类 |

### 应答

| 字段      | 类型    | 含义 |
| --------- | ------- | ---- |
| top_types | List of |      |

### 注释

| 值   | 含义 |
| ---- | ---- |
| 0    | C端  |
| 1    | B端  |

### 请求例

```http
GET /adminsys/category/l1/list/?operator=1
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "result": 200,
        "top_types": [
            {
                "id": 6,
                "t_top_name": "废铁",
                "in_use": true,
                "operator": 1,
                "create_time": "1543906611",
                "icon": null,
                "icon_selected": null,
                "ordering": 10,
                "description": "",
                "display": false
            },
            {
                "id": 14,
                "t_top_name": "有色金属",
                "in_use": true,
                "operator": 1,
                "create_time": "1543907051",
                "icon": null,
                "icon_selected": null,
                "ordering": 9,
                "description": "",
                "display": false
            },
        ]
    },
    "context": null
}
```

# 获取二级品类的列表

### URL

GET /adminsys/category/l2/list/

### 请求参数

| 参数名称 | 类型        | 含义         |
| -------- | ----------- | ------------ |
| unbound  | nullboolean | 未绑定       |
| id       | Int         | 顶级品类的ID |

### 应答

| 字段      | 类型    | 含义 |
| --------- | ------- | ---- |
| sub_types | List of |      |

### 注释

unbound

```
TRUE_VALUES = {
    't', 'T',
    'y', 'Y', 'yes', 'YES',
    'true', 'True', 'TRUE',
    'on', 'On', 'ON',
    '1', 1,
    True
}

FALSE_VALUES = {
        'f', 'F',
        'n', 'N', 'no', 'NO',
        'false', 'False', 'FALSE',
        'off', 'Off', 'OFF',
        '0', 0, 0.0,
        False
    }
    
NULL_VALUES = {'null', 'Null', 'NULL', '', None}
```

| 值                  | 含义     |
| ------------------- | -------- |
| TRUE_VALUES中的元素 | 已经绑定 |
| FALSE_VALUE中的元素 | 没有绑定 |
| NULL_VALUES         | 值为空   |

### 请求例

```http
GET /adminsys/category/l2/list/?unbound=T&id=6
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "result": 200,
        "sub_types": [
            {
                "id": 114,
                "unit": 1,
                "t_sub_name": "测试",
                "in_use": true,
                "price_default_flow": "0.000",
                "price_default_fix": "0.000",
                "create_time": "1548430595",
                "update_time": "1552312816",
                "to_kg_scale": "1.0000",
                "has_tax": true
            },
            {
                "id": 115,
                "unit": 2,
                "t_sub_name": "测试",
                "in_use": true,
                "price_default_flow": "0.000",
                "price_default_fix": "0.000",
                "create_time": "1548430616",
                "update_time": "1552312816",
                "to_kg_scale": "1.0000",
                "has_tax": true
            }
        ]
    },
    "context": null
}
```

# 对B端/C端的顶级品类进行增删改的接口

### URL

POST /adminsys/category/l1/

### 请求参数

| 参数名称 | 类型          | 含义           |
| -------- | ------------- | -------------- |
| top_type | Flatten(DICT) | 新增的品类信息 |

### 应答

| 参数名称 | 类型 | 含义         |
| -------- | ---- | ------------ |
| id       | Int  | 顶级品类的ID |

### 请求例

```http
POST /adminsys/category/l1/
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data": {
		"top_type": {
			"t_top_name": "废铜",
			"operator": 1,
			"icon_selected": null,
			"description": "就是废铁",
			"display": false,
			"ordering": 1
		}
	}
}

```

### 应答例

{
    "version": "2.0",
    "response": {
        "result": 200,
        "id": 49
    },
    "context": null
}

*****

### URL

```
PUT /adminsys/category/l1/
```

### 请求参数

| 参数名称 | 类型 | 含义             |
| -------- | ---- | ---------------- |
| id       | Int  | 顶级品类ID       |
| update   | DICT | 更新的品类的信息 |

### 应答

无

### 请求例

```http
PUT /adminsys/category/l1/
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data":{
			"id":49,
			"update":{
						"t_top_name": "废铜烂铁",
						"operator": 1,
						"icon_selected": null,
						"description": "就是废铁",
						"display": false,
						"ordering": 3
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

****

### URL

DELETE   /adminsys/category/l1/?id=6

### 请求参数

| 参数名称 | 类型 | 含义           |
| -------- | ---- | -------------- |
| id       | Int  | 要删除的品类ID |

### 应答

无

### 请求例

```http
DELETE /adminsys/category/l1/?id=49
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

此处的删除是软删除，品类数据不会被删除掉，而是通过修改品类是否在使用的状态来判断该品类是否存在。

delete是将in_use =True 改成 False，前端将不展示False的这条数据。

# B端/C端二级品类增删改的接口

### URL

POST  /adminsys/category/l2/

### 请求参数

| 参数名称 | 类型 | 含义                       |
| -------- | ---- | -------------------------- |
| sub_type | DICT | 要增加的二级品类的商品信息 |

### 应答

| 响应参数 | 类型 | 含义       |
| -------- | ---- | ---------- |
| id       | Int  | 二级品类ID |

### 请求例

```http
POST /adminsys/category/l2/
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"sub_type":{
				"toptype_b_id":8,
				"unit":"2",
                "t_sub_name": "葵花皮皮2",
                "in_use": true,
                "price_default_flow": "15.000",
                "price_default_fix": "16.000",
                "update_time": "1552312816",
                "to_kg_scale": "1.0000",
                "has_tax": true
            }
}
}
```

### 应答例

{
    "version": "2.0",
    "response": {
        "result": 200,
        "id": 137
    },
    "context": null
}

****

### URL	

PUT /adminsys/category/l2/

### 请求参数

| 参数名称      | 类型    | 含义                     |
| ------------- | ------- | ------------------------ |
| id            | Int     | 二级品类的ID             |
| update        | DICT    | 要更新的二级品类的信息   |
| refresh_price | Boolean | 是否刷新价格(默认不刷新) |

### 应答

无

### 请求例

```http
PUT /adminsys/category/l2/
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"id":8,
		"update":{
				"unit":1,
                "t_sub_name": "葵花皮皮3",
                "in_use": true,
                "price_default_flow": "0.000",
                "price_default_fix": "0.000",
                "create_time": "1548430595",
                "update_time": "1552312816",
                "to_kg_scale": "1.0000",
                "has_tax": "false"
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

修改接口的update内的所有字段均为可选，更新方式为增量式更新

例如：update下不含unit，则该次更新不对数据库中对应数据的unit做更新。

****

### URL

DELETE  /adminsys/category/l2/

### 请求参数

| 参数名称 | 类型 | 含义             |
| -------- | ---- | ---------------- |
| id       | Int  | 二级品类的商品ID |

### 应答

无

### 请求例

```http
DELETE /adminsys/category/l2/?id=8

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

此处的删除是软删除，品类数据不会被删除掉，而是通过修改品类是否在使用的状态来判断该品类是否存在。

delete是将in_use =True 改成 False，前端将不展示False的这条数据。

### B端/C端的顶级品类排序接口

### URL

POST /adminsys/category/l1/ordering/

### 请求参数

| 参数名称 | 类型   | 含义         |
| -------- | ------ | ------------ |
| oo       | Choice | 订单操作     |
| id       | Int    | 顶级品类的ID |

### 应答

无

### 注释

| 值   | 含义 |
| ---- | ---- |
| -1   | 下移 |
| 1    | 上移 |

### 请求例

```http
POST /adminsys/category/l1/ordering/
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"id":36,
		"oo":-1
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

增加接口的post内的所有的字段均是必填字段，通过修改这个oo的值来改变该商品的一个排序位置。

# B端/C端二级品类排序接口

### URL

POST /adminsys/category/l2/ordering/

### 请求参数

| 参数名称 | 类型   | 含义         |
| -------- | ------ | ------------ |
| oo       | Choice | 订单操作     |
| id       | Int    | 顶级品类的ID |

### 应答

无

### 注释

| 值   | 含义 |
| ---- | ---- |
| -1   | 下移 |
| 1    | 上移 |

### 请求例

```http
POST /adminsys/category/l2/ordering/
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"id":9,
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

### 注释

增加接口的post内的所有的字段均是必填字段，通过修改这个oo的值来改变该商品的一个排序位置。

二级品类要想通过post来新增数据的时候要满足两个条件，自身的is_use和其父（顶级品类）的is_use必须是true才能增加成功。

# 获取品类回收站列表

### URL

GET  /adminsys/category/recycle_bin/

### 请求参数

| 参数名称       | 类型 | 含义                      |
| -------------- | ---- | ------------------------- |
| recycle_bin_id | Int  | 回收站的ID                |
| toptype        | Int  | B端商品品类的ID(默认None) |

### 响应参数

| 响应字段 | 类型 | 含义             |
| -------- | ---- | ---------------- |
| products | DICT | 业务品类绑定信息 |

### 请求例

```http
GET /adminsys/category/recycle_bin/?recycle_bin_id=1&toptype_id=12/
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "products": [
            {
                "p_type__id": 119,
                "p_type__t_sub_name": "新版本",
                "price": "0.000",
                "modified_time": "1554098348",
                "p_type__unit": 2,
                "p_type_id": 119,
                "recycle_bin_id": 1,
                "p_type__to_kg_scale": "1.0000"
            },
            {
                "p_type__id": 104,
                "p_type__t_sub_name": "断桥铝",
                "price": "5.500",
                "modified_time": "1554098347",
                "p_type__unit": 1,
                "p_type_id": 104,
                "recycle_bin_id": 1,
                "p_type__to_kg_scale": "1.0000"
            },
            {
                "p_type__id": 105,
                "p_type__t_sub_name": "杂铝",
                "price": "5.500",
                "modified_time": "1554098347",
                "p_type__unit": 1,
                "p_type_id": 105,
                "recycle_bin_id": 1,
                "p_type__to_kg_scale": "1.0000"
            },     
        ],
        "result": 200
    },
    "context": null
}
```

# 未绑定品类的回收站接口

### URL

GET  /adminsys/category/recycle_bin/unbound/

### 请求参数

| 参数名称       | 类型 | 含义                      |
| -------------- | ---- | ------------------------- |
| recycle_bin_id | Int  | 回收站的ID                |
| toptype        | Int  | B端商品品类的ID(默认None) |

### 响应参数

| 响应字段 | 类型 | 含义                  |
| -------- | ---- | --------------------- |
| products | DICT | B端未绑定二级品类信息 |

### 请求例

```http
GET /adminsys/category/recycle_bin/unbound/?recycle_bin_id=19
```

### 应答例

暂无

# 品类回收站增删改的接口

### URL

POST  /adminsys/category/recycle_bin/product/

### 请求参数

| 参数名称 | 类型 | 含义                   |
| -------- | ---- | ---------------------- |
| product  | DICT | 要增加的回收站品类信息 |

### 应答

| 响应字段 | 类型 | 含义       |
| -------- | ---- | ---------- |
| id       | Int  | 新的品类ID |

### 请求例

```http
POST /adminsys/category/recycle_bin/product/?user_sid=foch09x9nbgmb6q6ee1s48dnkedkqrvv
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"product":{
				"p_type__id": 42,
                "p_type__t_sub_name": "测试BPTB",
                "price": "1.200",
                "p_type__unit": 3,
                "p_type_id": 6,
                "recycle_bin_id": 1,
                "p_type__to_kg_scale": "1.0000"
		}
	}
}

```

### 应答例

{
    "version": "2.0",
    "response": {
        "result": 200,
        "id": 1991
    },
    "context": null
}

### URL

PUT  /adminsys/category/recycle_bin/product/

### 请求参数

| 参数名称 | 类型 | 含义                 |
| -------- | ---- | -------------------- |
| id       | Int  | 已绑定的二级品类的ID |
| update   | DICT | 要更新的品类信息     |

### 响应参数

无

### 请求例

```http
POST /adminsys/category/recycle_bin/product/?user_sid=foch09x9nbgmb6q6ee1s48dnkedkqrvv
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"id":562,
		"update":{
				"p_type__id": 42,
                "p_type__t_sub_name": "测试BPTB",
                "price": "1.200",
                "p_type__unit": 3,
                "p_type_id": 6,
                "recycle_bin_id": 2,
                "p_type__to_kg_scale": "1.0000"
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

### URL

DELETE  /adminsys/category/recycle_bin/product/

### 请求参数

| 参数名称 | 类型 | 含义                 |
| -------- | ---- | -------------------- |
| id       | Int  | 已绑定的二级品类的ID |

### 响应参数

无

### 请求例

```http
GET /adminsys/category/recycle_bin/product/?user_sid=foch09x9nbgmb6q6ee1s48dnkedkqrvv&id=562
```

### 应答例

{
    "version": "2.0",
    "response": {
        "result": 200
    },
    "context": null
}