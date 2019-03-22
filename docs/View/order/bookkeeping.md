# 记账相关视图

## BookkeepingView

记账详情视图

### 视图表

| 字段名称 | 类型                                                         | 含义         |
| -------- | ------------------------------------------------------------ | ------------ |
| id       | PK                                                           | 主键(只读)   |
| p_type   | FK of [ProductSubType](/View/category/category/#productsubtypeview) | 品类ID       |
| oid      | FK of OrderInfo                                              | 订单ID(只读) |
| quantity | Decimal                                                      | 数量         |
| price    | Decimal                                                      | 总价(只读)   |

