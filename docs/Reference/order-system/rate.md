# 用户评价

## 获取评价标签

### URL

/order/c/rate/label/

### HTTP请求方式

__GET__

### HTTP请求参数

无

### HTTP响应参数

| 参数名称 | 参数类型 | 参数描述 |
| -------- | -------- | -------- |
| result   | Int      | 请求结果 |
| labels   | List     | 标签列表 |

### API 注释

result含义：

| 值   | 意义     |
| ---- | -------- |
| 200  | 请求成功 |
| 500  | 未知错误 |

### 示例

__请求__

```http
GET /order/c/rate/label/
```

__响应__

```json
{
    "response": {
        "result": 200,
        "labels": [
            {
                "id": 1,
                "label": "价格合理",
                "create_time": "15003240530"
            },
            {
                "id": 2,
                "label": "取货太慢",
                "create_time": "15002034025"
            }, ...
        ]
    }
}
```

## 提交评价

### URL

/order/c/rate/

### HTTP请求方式

__POST__

### HTTP请求参数

| 参数名称  | 参数类型         | 参数描述         |
| --------- | ---------------- | ---------------- |
| rank      | Int              | 1-5，星级        |
| label_ids | List of label id | 标签id列表       |
| order     | Order Id         | 订单ID           |
| comments  | String           | 评论内容（可选） |

### HTTP响应参数

| 参数名称 | 参数类型 | 参数描述 |
| -------- | -------- | -------- |
| result   | Int      | 请求结果 |

### API 注释

result含义：

| 值   | 意义             |
| ---- | ---------------- |
| 200  | 请求成功         |
| 3401 | 订单不属于该用户 |
| 3403 | 订单状态非完成   |
| 500  | 未知错误         |

### 示例

__请求__

```json
{
    "user_sid": "1234baedlkjfad",
    "data": {
        "rank": 5,
        "comments": "非常好",
        "label_ids": [1, 2],
        "order": 132,
    }
}
```

__响应__

```json
{
    "response": {
        "result": 200
    }
}
```

