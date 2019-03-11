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

