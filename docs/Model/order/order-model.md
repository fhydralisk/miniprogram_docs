#  订单（我的投递）模型

## OrderInfo 余额明细

### 模型定义

| 字段          | 类型   | 含义           | 是否私有 | 读/写 |
| ------------- | ------ | -------------- | -------- | ----- |
| id            | Int    | 订单唯一标识符 |          | R     |
| create_time   |Long    | 产生的时间戳   |          | R      |
| o_state       | Int   | 订单状态      |         | R         |
| amount        | float  |  订单金额        |       | R     |
| uid_c           | FK     | 对应客户         |        | R   |
| uid_b           | FK     | 对应回收员         |        | R   |
| c_delivery_info | [UserDeliveryInfo](/Model/user/delivery_model/) | 客户收货信息 | | R |

*注释*

o_state

| 值 | 含义|
|----|----|
| 0  | 订单发起 |
| 1  |订单被接收|
| 2 | 订单取消 |
| 3 | 订单完成   |