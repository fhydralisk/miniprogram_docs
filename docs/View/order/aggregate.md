# 订单记账聚合视图

## OrderBookkeepingAggregateListView

记账聚合列表视图

### 视图表

| 字段名称       | 类型                                  | 含义     |
| -------------- | ------------------------------------- | -------- |
| total_quantity | Decimal                               | 总数量   |
| total_price    | Decimal                               | 总金额   |
| aggregates     | List of OrderBookkeepingAggregateView | 二级聚合 |

## OrderBookkeepingAggregateView

记账聚合视图

### 视图表

| 字段名称 | 类型                                                         | 含义     |
| -------- | ------------------------------------------------------------ | -------- |
| quantity | Decimal                                                      | 数量     |
| price    | Decimal                                                      | 金额     |
| top_type | [ProductTopTypeView](/View/category/category/#producttoptypeview) | 顶级品类 |
| sub_type | [ProductSubTypeView](/View/category/category/#productsubtypeview) | 二级品类 |
| unit     | PK of ProductUnit                                            | 单位id   |

*注释*

如果按二级品类进行汇总，则unit字段存在于sub_type中

-------

## AggOperationChoice

聚合方式

### 值表

| 值             | 说明                           |
| -------------- | ------------------------------ |
| subtype_b      | 按2级品类汇总，返回B端顶级品类 |
| subtype_c      | 按2级品类汇总，返回C端顶级品类 |
| toptype_b      | 按B端1级品类汇总               |
| toptype_b_unit | 按B端1级品类及单位汇总         |
| toptype_c      | 按C端1级品类汇总               |
| toptype_c_unit | 按C端1级品类及单位汇总         |
| unit           | 按单位汇总                     |

例如，选择agg_op=toptype_b_unit，则统计记账中1级品类中各个单位的价格、数量；选择agg_op=unit则只统计各单位的数量、价格，忽略品类。