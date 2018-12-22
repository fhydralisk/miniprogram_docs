# 用户认证

## 获取已提交的认证照片

### URL
/user/validate/fetch_photo/

### HTTP请求方式
__GET__

将请求参数通过URI发送

### HTTP请求参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid	     		| String 				| 会话ID
t_photo					| Int					| 照片类型 

### HTTP响应

图片二进制流或通过HTTP状态码返回错误。

HTTP状态码：

值		|意义
--------|--------
200		|获取成功，数据返回
400		|请求有误
401		|user_sid错误
404		|用户未上传该照片
500		|未知错误

### API注释

**t_photo**取值含义

值		|意义
--------|--------
0		|手持证件照
1		|身份证正面照

### 示例

__请求__

/user/validate/fetch_photo/?user_sid=abc1323343sxa3vm&t_photo=0

__响应__

![imagine](img/license.jpg)

------------------------------------------------------------------------------

## 提交认证照片

### URL

/user/validate/submit_photo/

### HTTP请求方式
__POST FORM DATA__; name=**v_photo**

user_sid和t_photo通过URI发送，图片数据通过POST二进制流发送。
<!-- Apache LimitRequestBody Directive 限制POST大小 -->

### HTTP请求参数

如下参数通过URI传递

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid	     		| String 				| 会话ID
t_photo					| Int					| 照片类型 

图片通过POST传送

### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
result		     		| Int	 				| 上传结果代码
photo_id	| Int 	| 照片ID 

### API注释


result取值含义：

值		|意义
--------|--------
200		|上传成功
400		|请求有误
401	|已提交审核，无法更改
403		|图片有误
404		|未找到user_sid，可能已过期
500		|未知错误

### 示例

__请求__

```http
POST /user/validate/submit_photo/?user_sid=abc1323343sxa3vm&t_photo=1
Content-Type: multipart/form-data; boundary=----------------------------7db372eb000e2
Content-Length: 1017

----------------------------7db372eb000e2
Content-Disposition: form-data; name="v_photo"; filename="photo.jpg"
Content-Type: image/jpeg

(图片数据）
-------------------------------7db372eb000e2--

```

__响应__

```json
{
    "version": "0.1",
    "response": {
        "photo_id": 19,
        "result": 200
    },
    "context": null
}
```

-----------------------------------------------------------------------------

## 删除认证照片

/user/validate/delete_photo/

### HTTP请求方式
__GET__

请求参数通过URI发送

### HTTP请求参数

如下参数通过URI传递

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid	     		| String 				| 会话ID
t_photo				| Int					| 照片类型 

### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
result		     		| Int	 				| 状态码 

### API注释


result取值含义：

值		|意义
--------|--------
200		|删除成功
400		|请求有误
401	|已提交审核，无法更改
404		|未找到user_sid
500		|未知错误

### 示例

__请求__

```http
GET /user/validate/delete_photo/?user_sid=abc1323343sxa3vm&t_photo=1
```

__响应__
```json
{
    "version": "0.1",
    "response": {
        "result": 200
    },
    "context": null
}

```

---------

## 提交认证信息

### URL

/user/validate/submit_info/

### HTTP请求方式
__POST__

要求数据格式为JSON

### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid	     		| String 				| 会话ID
name                    | String                | 姓名
idcard_number           | String                | 身份证号


### HTTP响应参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
result		     		| Int	 				| 状态码



**result**取值含义：

值		|意义
--------|--------
200		|请求成功
400		|请求有误
401	|已经提交审核，无法更改
404		|未找到user_sid，可能已过期
500		|未知错误


### 示例

__请求__
```json
{
	"data":{
		"user_sid":	"c65fa1c5-0510-11e9-8bd6-6c96cfdf6ce7",
		"name": "xxx",
		"idcard_number": "122222"
	}
}
```
__响应__

```json
{
    "version": "0.1",
    "response": {
        "result": 200
    },
    "context": null
}
```



-----------------------------------------------------------------------------

## 获取用户认证信息

### URL
/user/validate/fetch_info/

### HTTP请求方式
__GET__

请求参数通过URI发送

### HTTP请求参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
user_sid	     		| String 				| 会话ID

### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
validate_obj			|  Object	| 认证对象
validate_photos_uploaded	| List of Int	| 已上传的认证照片类型 
result	| Int	| 状态代码 

### API注释

validate_obj

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
id			|  Int	| 数据库唯一标示
name	| String	| 姓名
idcard_number	| String	| 身份证号
validate_status | Int  | 用户认证状态

validate_status

值|意义
----|--------------------
0 | 用户尚未提交认证审核申请
1 | 用户已提交认证审核申请，但审核尚未被处理
2 | 用户已提交认证审核申请，且审核已通过
3 | 用户已提交认证审核申请，但审核被拒绝

**result**取值含义：

| 值   | 意义                       |
| ---- | -------------------------- |
| 200  | 请求成功                   |
| 400  | 请求有误                   |
| 404  | 未找到user_sid，可能已过期 |
| 500  | 未知错误                   |

若**result**返回值不为200，则**validate_obj**为空或不存在。

### 示例

#### 首次进入该页面的用户

__请求__

```http
GET /user/validate/fetch_info/?user_sid=abc1323343sxa3vm
```

__响应__

```json
{
    "version": "0.1",
    "response": {
        "validate_photos_uploaded": [
            0,
            1
        ],
        "validate_obj": {
            "id": 8,
            "idcard_number": "122222",
            "name": "xxx",
            "validate_status": 1,
            "uid": 6
        },
        "result": 200
    },
    "context": null
}
```


-----------------------------------------------------------------------------



# 本页版本信息

## 版本号

0.1.5

## 上次更新时间

2018-5-16   14:00
