# 订单记账聚合视图

## OrderBookkeepingAggregateListView

| 字段名称       | 类型                                  | 含义     |
| -------------- | ------------------------------------- | -------- |
| total_quantity | Decimal                               | 总数量   |
| total_price    | Decimal                               | 总金额   |
| aggregates     | List of OrderBookkeepingAggregateView | 二级聚合 |

## OrderBookkeepingAggregateView

| 字段名称 | 类型                                                         | 含义     |
| -------- | ------------------------------------------------------------ | -------- |
| quantity | Decimal                                                      | 数量     |
| price    | Decimal                                                      | 金额     |
| top_type | [ProductTopTypeView](/View/category/category/#producttoptypeview) | 顶级品类 |
| sub_type | [ProductSubTypeView](/View/category/category/#productsubtypeview) | 二级品类 |
| unit     | PK of ProductUnit                                            | 单位id   |

*注释*

如果按二级品类进行汇总，则unit字段存在于sub_type中