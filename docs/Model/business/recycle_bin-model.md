#  回收站

## RecycleBin 回收站

### 模型定义

| 字段          | 类型   | 含义           | 是否私有 | 读/写 |
| ------------- | ------ | -------------- | -------- | ----- |
| id            | Int    | 回收站唯一标识符 |          | R     |
| create_time   |Long    | 产生的时间戳   |          | R      |
| pn            | String  | 回收站电话   |           | R     |
| r_b_type       | Int   | 回收站累型      |         | R         |
| GPS_L         | float  |  经度        |       | R     |
| GPS_A           | float  | 纬度         |        | R   |
| rb_name         | String |  回收站名         |        | R   |
| location_desc | String    | 回收站地点描述 | | R |

*注释*

**r_b_type**<a name="r_b_type"></a>

| 值 | 含义|
|----|----|
| 0  | 固定站 |
| 1  |流动站|

type_list  (C端用，用来表述各种类的信息,主要用于固定站)

参数名称					|参数类型					|参数描述
------------------------|-----------------------|-------------------
type_id                 |  Int                  | 种类对应id
c_type             	    |   String              | 类型名
min_price                | Float                  | 该回收站对该品类的最低价格
max_price               | Float                 | 该回收站对该品类的最高价格
