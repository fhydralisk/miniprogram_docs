# 用户收货地址

## 用户提交收货地址

### URL
/order/operate/submit_delivery_info/

### HTTP请求方式
__POST JSON__


### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			    | String 	            | 16位会话ID
address                 | String                | 收货地址
contact_pn              | String                | 联系电话
contact                 | String                | 联系人（非必填）
house_number            | String                | 门牌号（非必填）


### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
result					| Int					| 请求结果

### API 注释

result含义：

值		|意义
--------|--------
200		|请求成功
404		|user_sid 不存在
500		|未知错误

### 示例

__请求__
```json
{
    "data": {
	"user_sid": "3fd60833-f543-11e8-9057-6c96cfdf6ce7",
	"address": "北京市海淀区xxxx",
	"contact_pn": "13800138000",
	"contact": "张xx",
	"house_number": "307"
    }
}
```

__响应__

```json
{
    "version": "0.1",
    "response": {
        "result": 200,
        "addr": {
            "id": 9,
            "address": "北京市海淀区xxxx",
            "contact": "张xx",
            "house_number": "307",
            "contact_pn": "13800138000"
        }
    },
    "context": null
}
```
--------------------------------------

## 获取用户收货地址

### URL
/order/obtain/delivery_info/

### HTTP请求方式
__GET__


### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			    | String 	          | 16位会话ID


### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
address_exist 			| Bool    				| 是否存在已有地址
delivery_info           | [UserDeliveryInfo](/Model/user/delivery_model/) | 投递列表
result					| Int					| 登录结果


### API 注释

result含义：

值		|意义
--------|--------
200		|请求成功
400     |请求错误或page超出总页数
404		|user_sid 不存在
500		|未知错误

### 示例

__请求__

/order/obtain/delivery_info/?user_sid=3fd60833-f543-11e8-9057-6c96cfdf6ce7

__响应__

```json
{
    "version": "0.1",
    "response": {
        "address_exist": true,
        "delivery_info": {
            "id": 9,
            "address": "北京市海淀区xxxx",
            "contact": "张xx",
            "house_number": "307",
            "contact_pn": "13800138000"
        },
        "result": 200
    },
    "context": null
}
```

```json
{
    "version": "0.1",
    "response": {
        "address_exist": false,
        "delivery_info": {
            "address": "",
            "contact": "",
            "house_number": "",
            "contact_pn": ""
        },
        "result": 200
    },
    "context": null
}
```

```json
{
    "version": "0.1",
    "response": {
        "address_exist": true,
        "delivery_info": {
            "address": "北京市海淀区xxxx",
            "contact": null,
            "house_number": null,
            "contact_pn": "13800138000"
        },
        "result": 200
    },
    "context": null
}
```