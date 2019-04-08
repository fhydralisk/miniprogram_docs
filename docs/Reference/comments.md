# API Reference说明

## 术语表

| 符号    | 含义   | 备注                                                 |
| ------- | ------ | ---------------------------------------------------- |
| Object  | 对象   | 作为响应或用作请求时以 Json 字典进行描述             |
| View    | 视图   |                                                      |
| Flatten | 扁平化 | 对多层级的字典格式的扁平处理，使得其更易被前端使用。 |

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

-------

## 扁平化

对关系型模型或JSON字典进行扁平化处理

### 处理方式

对所有的父节点非根节点的叶子节点(key_leaf: value, value为非集合对象)，寻找其祖先，并记录路径下的键，直到如下任意情况满足：

1. 祖先属于是根节点
2. 祖先为列表类集合节点中的元素

将路径(key_ancient, key_child1, key_child2, …, key_childn, key_leaf)下的所有键通过连接符(默认为'__')连接，构成新的键*key_flatted*=key_ancient\_\_key_child1\_\_key_child2\_\_…\_\_key_childn\_\_key_leaf

将新的key_flatted: value加入到祖先节点的父节点中

重复上述操作，直到所有的上述类型叶子节点都被处理，然后移除所有原有的节点。

### 示例1

示例1对关系模型视图[RecyclingStaffView](/View/business/recycle_bin/#recyclingstaffview)的序列化结果进行比对展示。

**关系模型非扁平序列化结果示例**

```json
{
    "id":4,
    "rs_name":"王五",
    "is_administrator":true,
    "modified_time":"1546794895",
    "user":{
        "id":15,
        "internal_name":"18888888890",
        "is_active":true,
        "role":1,
        "is_staff":false,
        "registered_date":"1548861789",
        "pn":"18888888890",
        "user_validate":null
    },
    "recycle_bin":{
        "id":11,
        "GPS_L":"121.5506260",
        "GPS_A":"39.0365320",
        "rb_name":"测试地点3",
        "r_b_type":0,
        "loc_desc":"辽宁省大连市测试区测试街道90号",
        "position_desc":null,
        "pn":"18888888890",
        "in_use":false
    }
}
```

**关系模型的扁平化示例**

```json
{
    "is_administrator":true,
    "id":4,
    "modified_time":"1546794895",
    "rs_name":"王五",
    "user__registered_date":"1548861789",
    "user__id":15,
    "user__pn":"18888888890",
    "user__is_staff":false,	
    "user__role":1,
    "user__user_validate":null,
    "user__is_active":true,
    "user__internal_name":"18888888890",
    "recycle_bin__GPS_L":"121.5506260",
    "recycle_bin__in_use":false,
    "recycle_bin__loc_desc":"辽宁省大连市测试区测试街道90号",
    "recycle_bin__r_b_type":0,
    "recycle_bin__position_desc":null,
    "recycle_bin__pn":"18888888890",
    "recycle_bin__GPS_A":"39.0365320",
    "recycle_bin__id":11,
    "recycle_bin__rb_name":"测试地点3"
}
```

### 示例2

**JSON非扁平结果示例**

```json
{
  "dict_contains_list": {
    "value": "test",
    "list": [
      {
        "key": "test_key1",
        "values": [1, 2, 3]
      },
      {
        "key": "test_key2",
        "values": [1, 2, 3]
      },
      {
        "key": "test_key3",
        "values": [1, 2, 3]
      }
    ]
  }
}
```

**扁平化结果**

```json
{
  "dict_contains_list__value": "test",
  "dict_contains_list__list": [
    {
      "key": "test_key1",
      "values": [1, 2, 3]
    },
    {
      "key": "test_key2",
      "values": [1, 2, 3]
    },
    {
      "key": "test_key3",
      "values": [1, 2, 3]
    }
  ]
}
```



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

2019-4-9