#  用户收货地址模型

## UserDeliveryInfo

### 模型定义

| 字段          | 类型   | 含义           | 是否私有 | 读/写 |
| ------------- | ------ | -------------- | -------- | ----- |
| id            | Int    | 数据库唯一标识符 |          | R     |
| uid           | FK     | 对应用户         |        | R   |
| address       | String | 收货地址       |          | R     |
| contact       | String | 联系人（可以为空）|         | R      |
| house_number  | String | 门牌号（可以为空）|       | R       |
| contact_pn    | String | 联系电话         |        | R     |
| in_use        | Bool   | 是否启用         |         | R   |

--------