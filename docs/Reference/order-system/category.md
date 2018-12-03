## 获取货物种类以及价格区间

### URL
/order/obtain/c_type/

### HTTP请求方式
__GET__


### HTTP请求参数

无

### HTTP响应参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
c_types                 |                       | 种类-价格区间
result					| Int					| 登录结果

c_types参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
c_type                  | String                | 种类
type_id                 | Int                   | 类型id
min_price               | Float                 | 最低价格
max_price               | Float                 | 最高价格
result					| Int					| 登录结果


### API 注释

result含义：

值		|意义
--------|--------
200		|请求成功
500		|未知错误

### 示例

__请求__

/order/obtain/c_type/

__响应__

```json
{
    "version": "0.1",
    "response": {
        "result": 200,
        "c_types": [
            {
                "c_type": "类型1",
                "min_price": 1,
                "max_price": 4,
                "type_id": 1
            },
            {
                "c_type": "类型2",
                "min_price": 2,
                "max_price": 3,
                "type_id": 2
            },
            {
                "c_type": "类型3",
                "min_price": 2,
                "max_price": 3,
                "type_id": 3
            }
        ]
    },
    "context": null
}
```
