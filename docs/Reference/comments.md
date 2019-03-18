# API Reference说明

## 术语表

| 符号   | 含义 | 备注                                     |
| ------ | ---- | ---------------------------------------- |
| Object | 对象 | 作为响应或用作请求时以 Json 字典进行描述 |
| View   | 视图 |                                          |

--------

## 接口规范(V2.0)

### JSON请求规范

- 通过API请求的数据位于data键下
- 前端上下文信息位于context键下，该信息将由后端服务器不做任何变更的返回。
- 用户会话user_sid位于字典根节点内。
- 版本信息位于version键下。*注：在API文档中，version键将被省略。*

**请求例**

```json
{
    "user_sid": "aassddffeeggaadd",
    "data": {
        "some_request": "some requesta data"
    },
    "context": {
        "save_me": "some data"
    },
    "version": "0.1"
}
```

### 其他规范

其他规范同V0.1版本

------

## 接口规范(V0.1)

### JSON请求规范

* 通过API请求的数据位于data键下
* 前端上下文信息位于context键下，该信息将由后端服务器不做任何变更的返回。
* 版本信息位于version键下。*注：在API文档中，version键将被省略。*

**请求例**

```json
{
    "data": {
        "user_sid": "aassddffeeggaadd"
    },
    "context": {
        "save_me": "some data"
    },
    "version": "0.1"
}
```



### JSON应答规范

* 应答数据位于response键下
  * response键下通常包含**result**键，**result**为200代表请求成功，其他值代表请求不成功，具体代码含义请参考各API **result**含义表
* 版本信息位于version键下
* 上下文信息位于context键下

**应答例**

```json
{
    "response": {
        "result": 200,
        "list": [1, 2, 3, 4]
    },
    "version": "0.1",
    "context": {
        "save_me": "some data"
    }
}
```



### HTTP GET 请求规范

* 请求参数通过URI发送，以**?**作为参数起始，**&**作为参数分隔，以key=***urlencode***(value)为参数赋值
* 以JSON返回的HTTP GET API，可以指定context=***urlencode***(json字典)的方式传递上下文，以其他方式返回的HTTP GET API将忽略context字段

**请求例**

```http
GET /somepath/somesystem/someapi/?user_sid=aassddffeeggaadd&context=%22save_me%22%3a+%22some+data%22
```

------------

# 本页版本信息

## 版本号

2.0.0

## 上次更新时间

2019-3-18