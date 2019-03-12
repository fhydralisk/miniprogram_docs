# 种类-品类视图

## ProductTopTypeView

### 视图表

| 字段名称         | 类型                                              | 含义         |
| ---------------- | ------------------------------------------------- | ------------ |
| id               | Long                                              |              |
| t_top_name       | String                                            | 名称         |
| in_use           | Boolean                                           | 是否使用     |
| description      | String                                            | 描述         |
| product_sub_type | List of [ProductSubTypeView](#productsubtypeview) | 二级品类列表 |
| price            | Decimal                                           | 均价         |
| price_max        | Decimal                                           | 最高价格     |
| price_min        | Decimal                                           | 最低价格     |

### 注释

price, price_max, price_min均为转换成公斤后的价格

-------

## ProductSubTypeView

### 视图表

| 字段名称           | 类型              | 含义                   |
| ------------------ | ----------------- | ---------------------- |
| id                 | Long              |                        |
| t_sub_name         | String            | 名称                   |
| unit               | FK ProductUnit    | 外键 ProductUnit id    |
| in_use             | Boolean           | 是否使用               |
| price_default_flow | Decimal           | 流动站缺省价格         |
| price_default_fix  | Decimal           | 固定站缺省价格         |
| price              | Decimal(Optional) | 价格（在特定接口存在） |

### 注释

price只在某些接口存在