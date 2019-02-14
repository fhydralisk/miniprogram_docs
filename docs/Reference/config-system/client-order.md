# 一键下单有关配置

## 预约下单时间

| 配置名称                          | 类型 | 说明                           | 权限 | 示例                               |
| --------------------------------- | ---- | ------------------------------ | ---- | ---------------------------------- |
| starttime.mkorder.client.ordersys | Int  | 以秒为单位的每日起始可预约时间 | Null | 36000 表示每日起始营业时间为10点整 |
| endtime.mkorder.client.ordersys   | Int  | 以秒为单位的每日起截止预约时间 | Null | 72000 表示每日停止营业时间为20点整 |
| interval.mkorder.client.ordersys  | Int  | 以秒为单位的预约粒度           | Null | 3600表示预约时间粒度为1小时        |
| days.mkorder.client.ordersys      | Int  | 以天为单位的最远预约天数       | Null | 2表示今天、明天                    |

