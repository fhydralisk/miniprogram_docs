# 质检单相关接口

## 获取装车单列表的接口

### URL

```http
GET /qc/qc_cred/list/
```

### 请求参数

| 参数名称                                            | 类型      | 含义                   |
| --------------------------------------------------- | --------- | ---------------------- |
| [qc_state](/View/qc/qc_credential/#qc_state_choice) | Choice    | 质检单状态（过滤器）   |
| [qc_type](/View/qc/qc_credential/#qc_type_choice)   | Choice    | 质检单类型（过滤器）   |
| start_time                                          | Timestamp | 质检开始时间（过滤器） |
| end_time                                            | Timestamp | 质检结束时间（过滤器） |
| truck                                               | String    | 车牌号（过滤器）       |
| load_id                                             | Int       | 装车单ID(过滤器)       |

### 应答

| 参数名称 | 类型                                                         | 含义       |
| -------- | ------------------------------------------------------------ | ---------- |
| qc_creds | List of [QCCredentialView](/View/qc/qc_credential/#qccredentialdetailview) | 质检单列表 |
| n_page   | Int                                                          | 页码数     |
| count    | Int                                                          | 数量       |

### 请求例

```http
GET /qc/qc_cred/list/?user_sid=lltemjbmsj1wl2vg1k4lf3rem9b88aq7
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "n_pages": 2,
        "count": 17,
        "qc_creds": [
            {
                "id": 1980,
                "load_id": 1986,
                "number_plate": "12333",
                "created_date": 1559203642,
                "closed_date": null,
                "qc_state": 0,
                "qc_type": 1
            },
            {
                "id": 1979,
                "load_id": 1986,
                "number_plate": "12333",
                "created_date": 1559203619,
                "closed_date": 1559203631,
                "qc_state": 2,
                "qc_type": 0
            }
        ],
        "result": 200
    },
    "context": null
}
```

---

### 开始质检接口

### URL

```http
POST /qc/qc_cred/
```

### 请求参数

| 参数名称                                          | 类型   | 含义       |
| ------------------------------------------------- | ------ | ---------- |
| [qc_type](/View/qc/qc_credential/#qc_type_choice) | Choice | 质检单类型 |
| lc_id                                             | Int    | 装车单ID   |

### 应答

无

### 请求例

```http
POST /qc/qc_cred/?user_sid=lltemjbmsj1wl2vg1k4lf3rem9b88aq7

{
	"data":{
		"qc_type":0,
		"lc_id":2000
	}
}
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "result": 200,
        "qc_id": 1987
    },
    "context": null
}
```

---

## 提交质检货物的接口

### URL

```http
POST /qc/qc_cred/detail/
```

### 请求参数

| 参数名称 | 类型                                                         | 含义     |
| -------- | ------------------------------------------------------------ | -------- |
| details  | List of [QCCredentialDetailView](/View/qc/qc_credential/#qccredentialdetailview) | 订单详情 |
| qc_type  | Choice                                                       | 订单类型 |
| id       | Int                                                          | 质检单ID |

### 应答

无

### 注释

id为开始质检接口返回的质检单qc_id

qc_type

| 值   | 含义   |
| ---- | ------ |
| 0    | 审核单 |
| 1    | 复核单 |

### 请求例

```HTTP
POST /qc/qc_cred/?user_sid=lltemjbmsj1wl2vg1k4lf3rem9b88aq7

{
	"data":{
		"qc_type":0,
		"id":1987,
		"details":[
			{
        "quantity":3.00,
        "category":2
		  }
		]
	}
}
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "result": 200
    },
    "context": null
}
```

