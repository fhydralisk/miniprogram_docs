# 回收站相关视图

### RecyclingStaffView

回收员视图

### 视图表

| 字段名称         | 类型                                                         | 含义           | 读写 |
| ---------------- | ------------------------------------------------------------ | -------------- | ---- |
| id               | Int                                                          | 主键           | R    |
| rs_name          | String                                                       | 回收员姓名     | RW   |
| is_administrator | Boolean                                                      | 回收站站长标志 | RW   |
| modified_time    | datetime                                                     | 修改时间       | R    |
| user             | [UserView](/View/user/user/#userview)                        | 用户视图       | R    |
| uid              | FK of user                                                   | 用户ID         | W    |
| recycle_bin_id   | FK of recycle_bin                                            | 回收站ID       | W    |
| recycle_bin      | [RecycleBinView](/View/business/recycle_bin/#recyclebinview) | 回收站视图     | R    |

------

## RecycleBinView

回收站视图

### 视图表

| 字段名称      | 类型                                                         | 含义                      | 读写 |
| ------------- | ------------------------------------------------------------ | ------------------------- | ---- |
| id            | Int                                                          | 主键                      | R    |
| GPS_L         | Decimal                                                      | 经度                      | RW   |
| GPS_A         | Decimal                                                      | 纬度                      | RW   |
| rb_name       | String                                                       | 回收站名称                | RW   |
| r_b_type      | recycle_bin_type_choice                                      | 回收站类型                | RW   |
| loc_desc      | String                                                       | 地点描述                  | RW   |
| position_desc | Dict                                                         | 地点词典                  | R    |
| pn            | String                                                       | 联系电话                  | RW   |
| in_use        | Boolean                                                      | 是否可用                  | RW   |
| admins        | List of String                                               | 管理员姓名列表            | R    |
| c_products    | List of [ProductTopTypeView](/View/category/category/#producttoptypeview) | 品类列表(以C端种类为顶级) | R    |
| b_products    | List of [ProductTopTypeView](/View/category/category/#producttoptypeview) | 品类列表(以B端种类为顶级) | R    |

----

## recycle_bin_type_choice

回收站类型Choice

### 值表

| 值   | 别名 | 含义   |
| ---- | ---- | ------ |
| 0    | fix  | 固定站 |
| 1    | flow | 流动站 |

