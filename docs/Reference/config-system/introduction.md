# 配置系统简介

配置系统用于获取所有前端需要的动态配置参数。例如缺省分页、一键下单的预约时间等。

## 获取配置接口

### URL

/config/

### HTTP请求方式
__GET__


### HTTP请求参数
| 参数名称    | 参数类型 | 参数描述   |
| ----------- | -------- | ---------- |
| config_name | string   | 配置名称   |
| user_sid    | string   | 用户会话ID |




### HTTP响应参数

| 参数名称   | 参数类型 | 参数描述 |
| ---------- | -------- | -------- |
| param_type | 参数类型 | 配置     |


### API 注释

result含义：

| 值   | 意义     |
| ---- | -------- |
| 200  | 请求成功 |
| 9404 | 无此配置 |
| 500  | 未知错误 |

### 示例

__请求__

http://127.0.0.1:8000/order/obtain/cancel_reason/

__响应__

```json
{
    "version": "0.1",
    "response": {
        "reasons": [
            {
                "id": 1,
                "reason": "原因1"
            },
            {
                "id": 2,
                "reason": "原因2"
            },
            {
                "id": 3,
                "reason": "原因3"
            }
        ],
        "result": 200
    },
    "context": null
}
```