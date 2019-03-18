# 装车单有关视图

## LoadingCredentialView

装车单视图

### 视图表

| 字段         | 类型                                                         | 含义           |
| ------------ | ------------------------------------------------------------ | -------------- |
| id           | Long                                                         | 主键           |
| truck        | String                                                       | 车牌号         |
| lc_state     | [lc_state_choice](#lc_state)                                 | 装车单当前状态 |
| rb_type      | [r_b_type_choice](/Model/business/recycle_bin-model/#r_b_type) | 回收站类型     |
| created_date | Timestamp                                                    | 创建日期       |
| cred_detail  | List of [LoadingCredentialDetailView](#loadingcredentialdetailview) | 装车单详情     |
| history      | List of {history_date: Timestamp, lc_state: [lc_state_choice](#lc_state)} | 装车单状态历史 |

### 注释

**lc_state**<a name="lc_state"></a>

| 值   | 含义     |
| ---- | -------- |
| 0    | 创建     |
| 1    | 已装车   |
| 2    | 已送达   |
| 3    | 已收货   |
| 4    | 过磅中   |
| 5    | 已审核   |
| 6    | 复核中   |
| 7    | 已复核   |
| 8    | 质检通过 |
| 100  | 旧版     |

## LoadingCredentialDetailView

装车单详情视图

### 视图表

| 字段     | 类型                                                         | 含义 |
| -------- | ------------------------------------------------------------ | ---- |
| id       | Loing                                                        |      |
| category | [ProductSubTypeView](/View/category/category/#productsubtypeview) |      |
| quantity | Decimal                                                      |      |
| price    | Decimal                                                      |      |

-------

## LoadingCredentialWithAggregateView

装车单及汇总视图

### 视图表

| 字段               | 类型                                                         | 含义       |
| ------------------ | ------------------------------------------------------------ | ---------- |
| loading_credential | [LoadingCredentialView](#loadingcredentialview)              | 装车单     |
| aggregate          | [OrderBookkeepingAggregateListView](/View/order/order/#orderbookkeepingaggregatelistview) | 装车单聚合 |

