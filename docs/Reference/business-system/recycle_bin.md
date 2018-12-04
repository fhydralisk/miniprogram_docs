# 获取回收站信息

## 获取最近几个(三个)回收站

### URL
/business/obtain/nearby/

### HTTP请求方式
__GET__


### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
lng			     		| Float          	    | 经度
lat                     | Float                 | 纬度

### HTTP响应参数
参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
closest 			  	| List       			| 最近的回收站
result					| Int					| 请求结果

### API 注释

closest内容

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
recycle_bin       	    | [RecycleBin](/Model/business/recycle_bin-model/) | 回收站信息详情
distance                | Float                  | 和用户的距离，以米为单位


result含义：

值		|意义
--------|--------
200		|请求成功
500		|未知错误

### 示例

__请求__

http://127.0.0.1:8000/business/obtain/nearby/?lng=116.308479&lat=39.983171

__响应__

```json
{
    "version": "0.1",
    "response": {
        "result": 200,
        "closest": [
            {
                "recycle_bin": {
                    "id": 1,
                    "GPS_L": 116.353455,
                    "GPS_A": 39.99606,
                    "rb_name": "回收站1",
                    "r_b_type": 0,
                    "loc_desc": "海淀区xxxxx",
                    "pn": "13145678910",
                    "type_list": [
                        {
                            "c_type": "类型1",
                            "min_price": 1,
                            "max_price": 4,
                            "type_id": 1
                        },
                        {
                            "c_type": "类型2",
                            "min_price": 2,
                            "max_price": 2,
                            "type_id": 2
                        },
                        {
                            "c_type": "类型3",
                            "min_price": 3,
                            "max_price": 3,
                            "type_id": 3
                        }
                    ]
                },
                "distance": 5060
            },
            {
                "recycle_bin": {
                    "id": 2,
                    "GPS_L": 116.39431,
                    "GPS_A": 39.949227,
                    "rb_name": "回收站2",
                    "r_b_type": 0,
                    "loc_desc": "海淀区xxxx",
                    "pn": "13245678910",
                    "type_list": [
                        {
                            "c_type": "类型1",
                            "min_price": 1,
                            "max_price": 1,
                            "type_id": 1
                        },
                        {
                            "c_type": "类型2",
                            "min_price": 3,
                            "max_price": 3,
                            "type_id": 2
                        },
                        {
                            "c_type": "类型3",
                            "min_price": 2,
                            "max_price": 2,
                            "type_id": 3
                        }
                    ]
                },
                "distance": 10131
            }
        ]
    },
    "context": null
}
```
--------------------------------------

## 获取一个回收站详情

### URL
/business/obtain/rb_detail/

### HTTP请求方式
__GET__


### HTTP请求参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
lng			     		| Float          	    | 经度
lat                     | Float                 | 纬度
rb_id                   | Int                   | 回收站id

### HTTP响应参数

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
recycle_bin       	    | [RecycleBin](/Model/business/recycle_bin-model/) | 回收站信息详情
distance                | Float                  | 和用户的距离，以米为单位


result含义：

值		|意义
--------|--------
200		|请求成功
500		|未知错误

### 示例

__请求__

http://127.0.0.1:8000/business/obtain/rb_detail/?lng=116.308479&lat=39.983171&rb_id=1

__响应__

```json
{
    "version": "0.1",
    "response": {
        "distance": 5060,
        "recycle_bin": {
            "id": 1,
            "GPS_L": 116.353455,
            "GPS_A": 39.99606,
            "rb_name": "回收站1",
            "r_b_type": 0,
            "loc_desc": "海淀区xxxx",
            "pn": "13145678910",
            "type_list": [
                {
                    "c_type": "类型1",
                    "min_price": 1,
                    "max_price": 4,
                    "type_id": 1
                },
                {
                    "c_type": "类型2",
                    "min_price": 2,
                    "max_price": 2,
                    "type_id": 2
                },
                {
                    "c_type": "类型3",
                    "min_price": 3,
                    "max_price": 3,
                    "type_id": 3
                }
            ]
        },
        "result": 200
    },
    "context": null
}
```