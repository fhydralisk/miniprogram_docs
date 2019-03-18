# 质检单聚合视图

## QCDetailAggregateListView

质检单详情聚合列表视图

### 视图表

| 字段           | 名称                                                    | 含义       |
| -------------- | ------------------------------------------------------- | ---------- |
| aggregates     | List of [QCDetailAggregateView](#qcdetailaggregateview) | 聚合列表   |
| total_price    | Decimal                                                 | 总价       |
| total_quantity | Decimal                                                 | 总数(可选) |

------

## QCDetailAggregateView

聚合列表

### 视图表

| 字段     | 名称                                                         | 含义     |
| -------- | ------------------------------------------------------------ | -------- |
| quantity | Decimal                                                      | 数量     |
| price    | Decimal                                                      | 价格     |
| sub_type | [ProductSubTypeView](/View/category/category/productsubtypeview) | 二级品类 |
| top_type | [ProductTopTypeView](/View/category/category/producttoptypeview) | 顶级品类 |
| unit     | PK of [ProductUnit](/View/category/unit/#productunit)        | 单位ID   |

### AggOperationChoice

聚合方式

### 值表

| 值           | 含义                |
| ------------ | ------------------- |
| subtype      | 按2级品类汇总       |
| toptype      | 按1级品类汇总       |
| toptype_unit | 按1级品类及单位汇总 |
| unit         | 按单位汇总          |

