# 单位接口

## 获取单位

### URL

*全局*

GET /category/unit/list/

### 请求参数

无

### 应答

| 字段名称 | 类型                                                        | 说明 |
| -------- | ----------------------------------------------------------- | ---- |
| units    | List of [ProductUnitView](/View/category/unit/#productunit) |      |

### 请求例

```http
GET /category/unit/list/
```

### 应答例

```json
{
    "version": "2.0",
    "response": {
        "units": [
            {
                "id": 1,
                "name": "公斤",
                "short_name": "kg",
                "scale": "1.000000000",
                "unit_class": 0
            },
            {
                "id": 2,
                "name": "个",
                "short_name": "pic",
                "scale": "1.000000000",
                "unit_class": 2
            }
        ],
        "result": 200
    },
    "context": null
}
```

---

