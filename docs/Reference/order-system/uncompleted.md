# 未完成订单

## 获取客户为完成订单

### URL
order/obtain/uncompleted/

### HTTP请求方式
__GET__


### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			    | String 	          | 16位会话ID


### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
exist        			| Bool    				| 该客户是否存在未完成订单
delivery_info           | [Order](/Model/order/order-model/) | 订单详情
result					| Int					| 登录结果


### API 注释

result含义：

值		|意义
--------|--------
200		|请求成功
404		|user_sid 不存在
500		|未知错误

### 示例

__请求__

/order/obtain/uncompleted/?user_sid=3fd60833-f543-11e8-9057-6c96cfdf6ce7

__响应__

```json
{
    "version": "0.1",
    "response": {
        "exist": true,
        "result": 200,
        "uncompleted": {
            "location": "北京市海淀区xxxx",
            "id": 19,
            "create_time": "2018-12-03T18:46:04.119630+08:00",
            "o_state": 0,
            "c_delivery_info": {
                "id": 9,
                "address": "北京市海淀区xxxx",
                "contact": "张xx",
                "house_number": "307",
                "contact_pn": "13800138000"
            }
        }
    },
    "context": null
}
```

```json
{
    "version": "0.1",
    "response": {
        "exist": false,
        "result": 200,
        "uncompleted": {
            "o_state": null,
            "c_delivery_info": {
                "address": "",
                "contact": "",
                "house_number": "",
                "contact_pn": ""
            }
        }
    },
    "context": null
}
```