# 宝宝金交易

## 获取宝宝金收支明细

### URL
/wallet/transaction/list/history/

### HTTP请求方式
__GET__


### HTTP请求参数

| 参数名称       | 参数类型 | 参数描述                      |
| -------------- | -------- | ----------------------------- |
| user_sid       | String   | 16位会话ID                    |
| page           | Int      | 指定明细的页数，不传则默认为0 |
| count_per_page | Int      | 每页数量                      |

### HTTP响应参数
| 参数名称     | 参数类型                                                 | 参数描述 |
| ------------ | -------------------------------------------------------- | -------- |
| n_pages      | Int                                                      | 总页数   |
| transactions | List of [TransactionDetail](/Model/wallet/wallet-model/) | 明细列表 |
| result       | Int                                                      | 请求结果 |

### API 注释

该接口返回项目含交易状态的变化历史。create_time指代该交易的创建时间，history_date指代该交易进入当前状态的时间。

result含义：

| 值   | 意义                     |
| ---- | ------------------------ |
| 200  | 请求成功                 |
| 400  | 请求错误或page超出总页数 |
| 404  | user_sid 不存在          |
| 500  | 未知错误                 |

### 示例

__请求__

```http
GET /wallet/transaction/history/?user_sid=f4bd5621-f196-11e8-bb37-6c96cfdf6ce7&page=0&count_per_page=10
```

__响应__

```json
{
    "version": "0.1",
    "response": {
        "n_pages": 1,
        "result": 200,
        "transactions": [
            {
                "id": 3,
                "create_time": "15302342532",
                "history_date": "15325234234",
                "t_type": 1,
                "t_state": 1,
                "t_source": 2,
                "amount": "12.000",
                "user": 1
            },
            {
                "id": 3,
                "create_time": "15302342525",
                "history_date": "15325234523",
                "t_type": 1,
                "t_state": 2,
                "t_source": 2,
                "amount": "12.000",
                "user": 1
            }
        ]
    },
    "context": null
}
```

---------
## 获取宝宝金交易状态

### URL
/wallet/transaction/list/

### HTTP请求方式
__GET__


### HTTP请求参数

| 参数名称       | 参数类型                         | 参数描述                                             |
| -------------- | -------------------------------- | ---------------------------------------------------- |
| user_sid       | String                           | 16位会话ID                                           |
| page           | Int                              | 指定明细的页数，不传则默认为0                        |
| count_per_page | Int                              | 每页数量                                             |
| t_state        | Optional[, splitted List of Int] | 以逗号分隔的状态过滤条件，如无需过滤，不要填写该参数 |
| t_source       | Optional[, splitted List of Int] | 以逗号分隔的来源过滤条件，如无需过滤，不要填写该参数 |
| t_type         | Optional[, splitted List of Int] | 以逗号分隔的种类过滤条件，如无需过滤，不要填写该参数 |

### HTTP响应参数
| 参数名称     | 参数类型                                                 | 参数描述 |
| ------------ | -------------------------------------------------------- | -------- |
| n_pages      | Int                                                      | 总页数   |
| transactions | List of [TransactionDetail](/Model/wallet/wallet-model/) | 明细列表 |
| result       | Int                                                      | 请求结果 |

### API 注释

该接口与获取宝宝金收支明细接口有所不同，其返回内容不包含交易状态变化的条目，只返回交易的当前状态。

result含义：

| 值   | 意义                     |
| ---- | ------------------------ |
| 200  | 请求成功                 |
| 400  | 请求错误或page超出总页数 |
| 404  | user_sid 不存在          |
| 500  | 未知错误                 |

### 示例

__请求__

```http
GET /wallet/transaction/?user_sid=f4bd5621-f196-11e8-bb37-6c96cfdf6ce7&page=0&count_per_page=10&t_state=1,2
```

__响应__

```json
{
    "version": "0.1",
    "response": {
        "n_pages": 1,
        "result": 200,
        "transactions": [
            {
                "id": 3,
                "create_time": "15302342532",
                "t_type": 1,
                "t_state": 1,
                "t_source": 2,
                "amount": "12.000",
                "user": 1
            }
        ]
    },
    "context": null
}
```

------

## 发起提现申请

### URL

/wallet/transaction/draw/

### 请求方法

POST

### 请求参数

| 参数名称 | 参数类型 | 参数说明 |
| -------- | -------- | -------- |
| amount   | Decimal  | 金额     |

### 应答参数

| 名称     | 类型                    | 说明         |
| -------- | ----------------------- | ------------ |
| trans_id | FK of TransactionDetail | 宝宝金交易id |

### API 注释

发起提现申请，并冻结响应金额。用户不可在有提现申请的情况下再次发起。

__result__

| 值   | 说明                               |
| ---- | ---------------------------------- |
| 400  | 请求有误                           |
| 404  | 用户不存在                         |
| 1402 | 余额不足                           |
| 1403 | 有正在处理的交易，不能重复申请提现 |



### 示例

**请求**

```json
{
    "user_sid": "f4bd5621-f196-11e8-bb37-6c96cfdf6ce7",
    "data": {
        "amount": "10.000"
    }
}
```

**应答**

```json
{
    "response": {
        "result": 200,
        "trans_id": 23,
    },
    "version": "0.1"
}
```

