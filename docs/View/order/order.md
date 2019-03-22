# 订单视图

## OrderView

### 视图定义

| 字段名称           | 字段类型               | 含义 |
| ------------------ | ---------------------- | ---- |
| id                 | Long                   |      |
| create_time        | Timestamp              |      |
| grab_time          | Timestamp              |      |
| complete_time      | Timestamp              |      |
| o_state            | Int(order_stat_choice) |      |
| amount             | Decimal                |      |
| c_delivery_info    | UserDeliveryInfoView   |      |
| recycling_staff    | RecyclingStaffView     |      |
| time_remain        | Long                   |      |
| time_remain_b      | Long                   |      |
| target_time        | Timestamp              |      |
| order_picking_time | OrderPickingTimeView   |      |
| can_cancel_b       | Bool                   |      |
| budget             | Decimal                |      |
| delete_code        | Int                    |      |
| bookkeeping        | BookkeepingView        |      |
| customer_products  | CustomerProductView    |      |

## order_state_choice

订单状态集

### 值定义

| 值   | 含义   |
| ---- | ------ |
| 0    | 创建   |
| 1    | 已接单 |
| 5    | 待记账 |
| 2    | 被取消 |
| 3    | 已完成 |
| 4    | 已删除 |

## order_bookkeeping_type

订单记账类型

### 值定义

| 值   | 含义          |
| ---- | ------------- |
| 0    | 扫码记账      |
| 1    | 抢单记账      |
| 2    | 无C端手动记账 |

