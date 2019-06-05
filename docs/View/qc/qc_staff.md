# QC端相关视图

### QcStaffsView

质检员视图

| 字段名称         | 类型                                          | 含义         | 读写 |
| ---------------- | --------------------------------------------- | ------------ | ---- |
| id               | Int                                           | 质检员ID     | RW   |
| user             | [UserView](/View/user/user/#UserView)         | 用户视图     | RW   |
| user_id          | FK of user                                    | 用户ID       | W    |
| name             | String                                        | 质检员姓名   | RW   |
| join_date        | datetime                                      | 加入时间     | RW   |
| qc_place         | [QcPlaceView](/View/qc/qc_place/#QcPlaceView) | 质检场地     | R    |
| qc_place_id      | FK of qc_place                                | 质检场地ID   | W    |
| qc_role          | qc_role_choice                                | 质检员角色   | RW   |
| is_administrator | Boolean                                       | 是否是管理员 | RW   |

---

### qc_role_choice

---

质检员角色AliasChoice

### 值表

| 值   | alias(别名) | 含义   |
| ---- | ----------- | ------ |
| 0    | checker     | 质检员 |
| 1    | reviewer    | 复核员 |

