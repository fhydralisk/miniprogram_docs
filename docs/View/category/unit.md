# 单位视图

## ProductUnit

### 字段表

| 字段名称               | 类型    | 说明                 |
| ---------------------- | ------- | -------------------- |
| id                     | Long    |                      |
| name                   | String  | 中文名称             |
| short_name             | String  | 英文简称             |
| scale                  | Decimal | 基本公制单位转换系数 |
| unit_class             | Int     | 基本公制单位类型     |
| quantity_decimal_place | Int     | 数量小数点显示位数   |

### 注释

**unit_class**

| 值   | 含义               |
| ---- | ------------------ |
| 0    | 千克               |
| 1    | 立方米             |
| 2    | 无量纲（个、箱等） |

