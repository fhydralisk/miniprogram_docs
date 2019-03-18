# 质检单有关视图

## QCCredentialDetailFlatView

扁平化的质检单详情视图

### 视图表

| 字段名称              | 类型                   | 含义        |
| --------------------- | ---------------------- | ----------- |
| id                    | PK of QCCredential     | 主键        |
| category              | FK of QCProductSubType | QC品类主键  |
| category_name         | String                 | 2级品类名称 |
| category_toptype_name | String                 | 1级种类名称 |
| price                 | 总价                   | 总价        |
| quantity              | Decimal                | 数量        |

## QCCredentialDetailView

树形质检单详情视图

### 视图表

| 字段名称 | 类型                                                         | 含义     |
| -------- | ------------------------------------------------------------ | -------- |
| id       | PK of QCCredential                                           | 主键     |
| category | [QCProductSubTypeView](/View/category/category/#qcproductsubtypeview) | 品类视图 |
| price    | Decimal                                                      | 总价     |
| quantity | Decimal                                                      | 数量     |

-----

## QCCredentialView

质检单视图

### 视图表

| 字段名称          | 类型                                                      | 含义         |
| ----------------- | --------------------------------------------------------- | ------------ |
| id                | PK of QCCredentialView                                    | 主键         |
| load_id           | FK of LoadingCredential                                   | 对应装车单ID |
| number_plate      | String                                                    | 车牌号       |
| closed_date       | Timestamp                                                 | 完成时间     |
| created_date      | Timestamp                                                 | 创建时间     |
| qc_state          | [qc_state_choice](#qc_state_choice)                       | 质检状态     |
| qc_type           | [qc_type_choice](#qc_type_choice)                         | 质检种类     |
| credential_detail | [QCCredentialDetailFlatView](#qccredentialdetailflatview) |              |

### 注释

**qc_state_choice**<a name="qc_state_choice"></a>

| 值   | 含义     |
| ---- | -------- |
| 0    | 正在审核 |
| 1    | 审核通过 |
| 2    | 审核失败 |
| 3    | 取消     |

**qc_type_choice**<a name="qc_type_choice"></a>

| 值   | 含义   |
| ---- | ------ |
| 0    | 审核单 |
| 1    | 复核单 |

