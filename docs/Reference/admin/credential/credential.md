# 装车单相关接口

## 获取装车单列表(3-1-1)

### URL

GET /adminsys/credential/lc/list/

### 请求参数

| 参数名称           | 类型                  | 含义           |
| ------------------ | --------------------- | -------------- |
| user_sid           | String                | 会话           |
| page               | Int(Optional)         | 页码           |
| count_per_page     | Int(Optional)         | 每页条目数     |
| extra_filter       | String(Optional)      | 过滤器         |
| plate_number       | String(Optional)      | 汇总数         |
| is_qc_passed       | NullBoolean(Optional) | 是否通过了质检 |
| start_time_loading | Timestamp(Optional)   | 装车开始时间   |
| end_time_loading   | Timestamp(Optional)   | 装车结束时间   |
| start_time_qc      | Timestamp(Optional)   | 质检开始时间   |
| end_time_qc        | Timestamp(Optional)   | 质检结束时间   |
| recycle_bin_name   | String(Optional)      | 回收站名       |
| lc_qc_filter       | String(Optional)      | 质检员的名字   |
| id                 | Int(Optional)         | 装车单ID       |

### 应答

| 参数名称          | 类型 | 含义                 |
| ----------------- | ---- | -------------------- |
| n_pages           | Int  | 页码数               |
| credentials       | List | 装车单相关信息       |
| count_qc_password | Int  | 通过质检的装车单数量 |
| count_all         | Int  | 装车单总数量         |

### 注释

lc_x_qc__lc_state

| 值        | 含义       |
| --------- | ---------- |
| created   | 创建装车单 |
| loaded    | 已装车     |
| arrived   | 已送达     |
| received  | 已收货     |
| checking  | 过磅中     |
| checked   | 已审核     |
| reviewing | 复核中     |
| reviewed  | 已复核     |
| qc_passed | 检验通过   |



### 请求例

获取通过质检的装车单，每页3个，取第二页

```http
GET /adminsys/credential/lc/list/?page=1&count_per_page=3&lc_x_qc__lc_state=T
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "n_pages": 21,
        "credentials": [
            {
                "total_price_qc": 1111.0,
                "recycle_bin__r_b_type": "flow",
                "total_price": 79.2,
                "qc_passed_date": 1554120278,
                "user__recycling_staff_info__rs_name": "流三",
                "lc_x_qc__lc_state": "qc_passed",
                "trigger_alert": true,
                "id": 70,
                "truck__number_plate": "ZZZZZZ",
                "user__pn": "15666666666"
            },
            {
                "total_price_qc": 666.0,
                "recycle_bin__r_b_type": "flow",
                "total_price": 1332.0,
                "qc_passed_date": 1554120149,
                "user__recycling_staff_info__rs_name": "流三",
                "lc_x_qc__lc_state": "qc_passed",
                "trigger_alert": true,
                "id": 69,
                "truck__number_plate": "33333",
                "user__pn": "15666666666"
            },
            {
                "total_price_qc": 33.0,
                "recycle_bin__r_b_type": "flow",
                "total_price": 14.0,
                "qc_passed_date": 1554106512,
                "user__recycling_staff_info__rs_name": "流三",
                "lc_x_qc__lc_state": "qc_passed",
                "trigger_alert": true,
                "id": 68,
                "truck__number_plate": "AAA",
                "user__pn": "15666666666"
            }
        ],
        "count_all": 62,
        "count_qc_passed": 19,
        "result": 200
    },
    "context": null
}
```

## 装车单基本信息接口(3-1-1-1)

### URL

GET  /adminsys/credential/lc/

### 请求参数

| 参数名称 | 类型 | 含义     |
| -------- | ---- | -------- |
| id       | Int  | 装车单ID |

### 应答

| 参数名称   | 类型 | 含义           |
| ---------- | ---- | -------------- |
| credential | DICT | 装车单基本信息 |

### 请求例

获取id为70的装车单信息

```http
GET /adminsys/credential/lc/?id=70
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "credential": {
            "recycle_bin__r_b_type": "flow",
            "user__recycling_staff_info__rs_name": "流三",
            "lc_x_qc__lc_state": "qc_passed",
            "lc_x_qc__history": [
                {
                    "lc_state": "qc_passed",
                    "history_date": 1554120278
                },
                {
                    "lc_state": "reviewed",
                    "history_date": 1554120278
                },
                {
                    "lc_state": "reviewing",
                    "history_date": 1554120272
                },
                {
                    "lc_state": "checked",
                    "history_date": 1554120269
                },
                {
                    "lc_state": "checking",
                    "history_date": 1554120263
                },
                {
                    "lc_state": "arrived",
                    "history_date": 1554120252
                }
            ],
            "id": 70,
            "truck__number_plate": "ZZZZZZ",
            "user__pn": "15666666666"
        },
        "result": 200
    },
    "context": null
}
```

## 装车单详情接口(3-1-1-1)

### URL

GET  /adminsys/credential/lc/detail/list/

### 请求参数

| 参数名称 | 类型   | 含义     |
| -------- | ------ | -------- |
| id       | Int    | 装车单ID |
| user_sid | String | 会话     |

### 应答

| 参数名称  | 类型 | 含义           |
| --------- | ---- | -------------- |
| details   | List | 装车单详情信息 |
| aggregate | Dict | 总量           |

### 请求例

获取 id=56 的装车单的详细信息

```http
GET /adminsys/credential/lc/detail/list/?id=56
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "aggregate": {
            "aggregates": [
                {
                    "quantity": "50.000000",
                    "price": "50.000",
                    "unit": 2
                },
                {
                    "quantity": "96.420000",
                    "price": "96.420",
                    "unit": 1
                }
            ],
            "total_price": "146.420"
        },
        "result": 200,
        "details": [
            {
                "price": "50.000",
                "category__t_sub_name": "易拉罐",
                "unit_price": "1",
                "category__unit": 2,
                "category__toptype_b__t_top_name": "易拉ddd",
                "id": 112,
                "quantity": "50.000000"
            },
            {
                "price": "22.000",
                "category__t_sub_name": "测试123",
                "unit_price": "1",
                "category__unit": 1,
                "category__toptype_b__t_top_name": "易拉ddd",
                "id": 113,
                "quantity": "22.000000"
            },
            {
                "price": "37.870",
                "category__t_sub_name": "白料",
                "unit_price": "1",
                "category__unit": 1,
                "category__toptype_b__t_top_name": "杂料(塑)",
                "id": 114,
                "quantity": "37.870000"
            },
            {
                "price": "10.000",
                "category__t_sub_name": "其他杂料",
                "unit_price": "1",
                "category__unit": 1,
                "category__toptype_b__t_top_name": "杂料(塑)",
                "id": 115,
                "quantity": "10.000000"
            },
            {
                "price": "1.000",
                "category__t_sub_name": "红铜",
                "unit_price": "1",
                "category__unit": 1,
                "category__toptype_b__t_top_name": "有色金属B",
                "id": 116,
                "quantity": "1.000000"
            },
            {
                "price": "21.000",
                "category__t_sub_name": "黄铜",
                "unit_price": "1",
                "category__unit": 1,
                "category__toptype_b__t_top_name": "有色金属B",
                "id": 117,
                "quantity": "21.000000"
            },
            {
                "price": "4.550",
                "category__t_sub_name": "花料",
                "unit_price": "1",
                "category__unit": 1,
                "category__toptype_b__t_top_name": "杂料(塑)",
                "id": 118,
                "quantity": "4.550000"
            }
        ]
    },
    "context": null
}
```

### 一审和复审质检单详情(3-1-1-1)

### URL

GET  /adminsys/credential/qc/detail/list/

### 请求参数

| 参数名称 | 类型   | 含义       |
| -------- | ------ | ---------- |
| id       | Int    | 装车单ID   |
| qc_type  | Alias  | 质检单状态 |
| user_sid | String | 会话       |

### 应答

| 参数名称  | 类型 | 含义       |
| --------- | ---- | ---------- |
| detail    | Dict | 装车单详情 |
| aggregate | List | 总量       |

### 注释

qc_tyoe 两种情况

| 值     | 含义       |
| ------ | ---------- |
| check  | 第一次审查 |
| review | 复审       |

### 请求例

获取 装车单id=70 的第一次审查的质检单详情

```http
GET /adminsys/credential/qc/detail/list/?id=70&qc_type=check
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "aggregate": {
            "aggregates": [
                {
                    "quantity": "1111.000000",
                    "price": "1111.000",
                    "unit": 1
                }
            ],
            "total_price": "1111.000"
        },
        "result": 200,
        "details": [
            {
                "price": "1111.000",
                "unit_price": "1.000",
                "category__name": "件铝",
                "category__unit": 1,
                "category__toptype__t_top_name": "有色金属B",
                "id": 147,
                "quantity": "1111.000000"
            }
        ]
    },
    "context": null
}
```

## 邮件操作接口(3-1-1)

### URL

GET  /adminsys/credential/lc/operate/

### 请求参数

| 参数名称        | 类型   | 含义     |
| --------------- | ------ | -------- |
| credential_type | Choice | 单子类型 |
| operate         | Choice | 操作内容 |
| id              | Int    | 装车单id |
| user_sid        | String | 会话     |

### 应答

无

### 注释

credential_type

| 值   | 含义   |
| ---- | ------ |
| load | 装车单 |
| qc   | 质检单 |

operate

| 值       | 含义     |
| -------- | -------- |
| download | 下载汇总 |
| email    | 发送邮件 |
| refresh  | 刷新     |

### 请求例

```http
GET /adminsys/credential/lc/operate/?credential_type=qc&operate=email&id=69
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

### 注释

当进行下载时，会下载一个汇总表单

## 装车质检单下载接口(3-1-1)

### URL

GET  /adminsys/credential/lc/download/

### 请求参数

| 参数名称        | 类型              | 含义     |
| --------------- | ----------------- | -------- |
| id_list         | list              | 装车单id |
| credential_type | Choice            | 单子类型 |
| separated       | Boolean(Optional) | 是否压缩 |
| user_sid        | String            | 会话     |

### 应答

如果条件满足会直接下载

### 注释

credential

| 值   | 含义   |
| ---- | ------ |
| qc   | 质检单 |
| load | 装车单 |

### 请求例

下载装车单ID为69的装车单，不打包

```http
GET /adminsys/credential/lc/download/?id_list=69&credential_type=load&separated=True
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

会下载一个压缩包，解压之后就是需要的表单

## 获取装车单和质检单的汇总列表(3-1-2)

### URL

GET  /adminsys/credential/lc/agg/list/

### 请求参数

| 参数名称        | 类型                | 含义                   |
| --------------- | ------------------- | ---------------------- |
| agg_type        | Choice              | 按照什么方式汇总       |
| credential_type | Choice              | 单子类型               |
| start_time      | Timestamp(Optional) | 单子创建时间(用于过滤) |
| end_time        | Timestamp(Optional) | 单子截至时间(用于过滤) |
| page            | Int                 | 页码                   |
| count_per_page  | Int                 | 每页条目数             |
| user_sid        | String              | 会话                   |

### 应答

| 参数名称               | 类型 | 含义         |
| ---------------------- | ---- | ------------ |
| credentials_aggregated | List | 单子汇总信息 |

### 注释

agg_type

| 值    | 含义     |
| ----- | -------- |
| day   | 按天汇总 |
| week  | 按周汇总 |
| month | 按月汇总 |

credential_type

| 值   | 含义   |
| ---- | ------ |
| qc   | 质检单 |
| load | 装车单 |

### 请求例

获取每周质检单的汇总列表，获取第二页，每页两条

```http
GET /adminsys/credential/lc/agg/list/?credential_type=qc&agg_type=week&page=1&count_per_page=2
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "n_pages": 2,
        "credentials_aggregated": [
            {
                "agg_type": "week",
                "st_time": 1551621600,
                "ed_time": 1552226400,
                "price": "70.000"
            },
            {
                "agg_type": "week",
                "st_time": 1549807200,
                "ed_time": 1550412000,
                "price": "1249.000"
            }
        ],
        "result": 200
    },
    "context": null
}
```

### 装车单和质检单汇总的操作接口 (3-1-2)

### URL

GET  /adminsys/credential/lc/agg/operate/

### 请求参数

| 参数名称        | 类型      | 含义                  |
| --------------- | --------- | --------------------- |
| operate         | Choice    | 操作内容              |
| st_time         | Timestamp | 装车单/质检单开始时间 |
| agg_type        | Choice    | 汇总类型              |
| credential_type | Choice    | 单子类型              |

### 应答

如果时发邮件，会收到邮件信息

如果是下载，会下载对应的表单

### 注释

agg_type

| 值    | 含义     |
| ----- | -------- |
| day   | 按天汇总 |
| week  | 按周汇总 |
| month | 按月汇总 |



### 请求例

获取agg_type为week且st_time为1551621600的质检单，然后发邮件

```http
GET /adminsys/credential/lc/agg/operate/?credential_type=qc&operate=email&st_time=1551621600&agg_type=week
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

### 获取装车单/质检单的邮件列表

### URL

