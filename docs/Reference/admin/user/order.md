# 订单相关接口（2-4）

## 获取订单列表（2-4-1）

### URL

GET	/adminsys/order/list/

### 请求参数

| 参数名称        | 类型                | 含义                                     |
| --------------- | ------------------- | ---------------------------------------- |
| oeder_id        | Int(Optional)       | 订单ID                                   |
| start_time      | Timestamp(Optional) | 起始时间(过滤器)                         |
| end_time        | Timestamp(Optional) | 截止时间(过滤器)                         |
| contact         | String(Optional)    | 联系人新姓名或电话(过滤器)               |
| recycling_staff | String(Optional)    | 回收人员(默认为None)                     |
| include_deleted | Boolean(Optional)   | 是否包括已经删除的订单(过滤器,默认False) |
| r_b_type        | Alias               | 回收站类型                               |
| dispatch_filter | Choice              | 调度的过滤器                             |
| page            | Int(Optional)       | 页码(过滤器)                             |
| count_per_page  | Int(Optional)       | 每页条目数                               |

### 应答

| 参数名称            | 类型 | 含义               |
| ------------------- | ---- | ------------------ |
| count_flow          | Int  | 流动站订单数量     |
| count_fixed         | Int  | 固定站订单数量     |
| count_all           | Int  | 全部订单数量       |
| count_all_dispatch  | Int  | 被调度的订单数量   |
| count_need_dispatch | Int  | 需要调度的订单数量 |
| n_page              | Int  | 页码数             |
| orders              | List | 订单详情           |

### 注释

include_deleted

| 值    | 含义   |
| ----- | ------ |
| True  | 包括   |
| Flase | 不包括 |

r_b_type

| 值   | 含义   |
| ---- | ------ |
| fix  | 固定站 |
| flow | 流动站 |

dispatch_filter

| 值            | 含义     |
| ------------- | -------- |
| need_dispatch | 需要调度 |
| all_dispatch  | 全部调度 |

### 请求例

获取订单ID为823的订单信息

```http
GET /adminsys/order/list/?order_id=823
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "count_all_dispatch": 87,
        "count_fixed": 44,
        "count_need_dispatch": 0,
        "n_pages": 1,
        "count_flow": 213,
        "result": 200,
        "count_all": 340,
        "orders": [
            {
                "recycling_staff__rs_name": "王五",
                "recycling_staff__rs_pn": "18888888890",
                "o_state": "deleted",
                "budget": null,
                "time_remain": 0,
                "client": null,
                "create_time": 1554342354,
                "dispatch_state": "deleted",
                "id": 823
            }
        ]
    },
    "context": null
}
```

## 获取订单详情接口

### URL

GET	/adminsys/order/

### 请求参数

| 参数名称 | 类型 | 含义   |
| -------- | ---- | ------ |
| id       | Int  | 订单ID |

### 应答

| 参数名称 | 类型 | 含义                   |
| -------- | ---- | ---------------------- |
| order    | DICT | 【扁平化】订单详情信息 |

### 请求例

获取订单ID为823的订单详情

```http
GET /adminsys/order/?id=823
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "result": 200,
        "order": {
            "recycling_staff__rs_name": "王五",
            "recycling_staff__rs_pn": "18888888890",
            "o_state": "deleted",
            "budget": null,
            "time_remain": 0,
            "client": null,
            "create_time": 1554342354,
            "customer_products": [],
            "dispatch_state": "deleted",
            "id": 823,
            "history": [
                {
                    "loaded": false,
                    "o_state": "deleted",
                    "history_date": 1554364904
                },
                {
                    "loaded": false,
                    "o_state": "completed",
                    "history_date": 1554342354
                },
                {
                    "loaded": false,
                    "o_state": "pre_bookkeeping",
                    "history_date": 1554342354
                }
            ]
        }
    },
    "context": null
}
```

****

### URL

POST	/adminsys/order/

### 请求参数

| 参数名称        | 类型   | 含义              |
| --------------- | ------ | ----------------- |
| products        | List   | 商品的信息(C端的) |
| order_type      | Choice | 回收站类型        |
| c_delivery_info | DICT   | 用户收获信息      |

### 应答

| 参数名称 | 类型 | 含义   |
| -------- | ---- | ------ |
| id       | Int  | 订单ID |

### 注释

order_type

| 值   | 含义         |
| ---- | ------------ |
| 0    | fix(固定站)  |
| 1    | flow(流动站) |

### 请求例

```http
POST /adminsys/order/?user_sid=gil5zpkfse06cu414wdwwwfggint8ksy
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"products":[],
		"order_type":0,
		"c_delivery_info":{
			"address":"北京市五道口",
			"contact_pn":18888888890
		}
	}
}
```

### 应答例

{
    "version": "2.0",
    "response": {
        "result": 200,
        "id": 870
    },
    "context": null
}

## 订单调度接口

### URL

GET	/adminsys/order/dispatch/

### 请求参数

| 参数名称 | 类型 | 含义   |
| -------- | ---- | ------ |
| id       | Int  | 订单ID |

### 应答

| 参数名称      | 类型 | 含义     |
| ------------- | ---- | -------- |
| dispatch_info | DICT | 调度信息 |

### 请求例

获取订单ID为822的调度信息

```http
GET /adminsys/order/dispatch/?id=822&user_sid=v22qhig1oxxp8c12ww24lq8adzdpas15
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "dispatch_info": {
            "dispatched_time": 1555419978,
            "remark": "不错不错，味道好极了",
            "id": 1,
            "dispatcher__internal_name": "wxroot"
        },
        "result": 200
    },
    "context": null
}
```

---

### URL

POST	/adminsys/order/dispatch/

### 请求参数

| 参数名称      | 类型 | 含义     |
| ------------- | ---- | -------- |
| id            | Int  | 订单ID   |
| dispatch_info | DICT | 调度信息 |

### 应答

无

### 请求例

```http
POST /adminsys/order/dispatch/?id=564&user_sid=8p2r7n015e8y2i1awjdsylmw89uuot4o
Host:-
Content-Type:application/json
cache-control:no=cache
{
	"data":{
		"id":564,
		"dispatch_info":{
			"id":566,
			"remark":"不错不错，味道好极了",
			"order_id":566,
			"dispatcher_id":3
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

在post时，必须保证order_dispatch_info__isnull=True才能添加成功，即订单的的状态不能有操作，在被创建的时候才能被调度。

