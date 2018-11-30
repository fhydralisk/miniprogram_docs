# 获取用户信息

## 获取用户个人信息

### URL
/user/obtain/self_info/

### HTTP请求方式
__GET__


### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid			     		| String 	    | 16位会话ID

### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_info 			  	|  用户信息参数集 			| 用户信息参数集
is_validate             | Int                   |  该用户是否实名认证过
result					| Int					| 请求结果

### API 注释

user_info内容

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
id       			  	|  Int       			| 用户唯一标示ID
pn                       | String                   |  用户手机号
idcard_number           | String                | 用户身份证号
name                    | String                | 用户真实姓名

result含义：

值		|意义
--------|--------
200		|请求成功
404		|user_sid 不存在
500		|未知错误

### 示例

__请求__

/user/obtain/self_info/?user_sid=a81966ab-f2da-11e8-900b-6c96cfdf6ce7

__响应__

```json
{
    "version": "0.1",
    "response": {
        "user_info": {
            "id": 1,
            "pn": "13800138000",
            "name": "马腾飞",
            "idcard_number": "110xxxxxxxxxxxxxxx"
        },
        "is_validate": 1,
        "result": 200
    },
    "context": null
}
```
--------------------------------------