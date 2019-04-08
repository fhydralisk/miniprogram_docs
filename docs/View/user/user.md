# 用户相关视图

## UserView

用户视图

### 视图表

| 字段名称        | 类型             | 含义                 | 读写 |
| --------------- | ---------------- | -------------------- | ---- |
| id              | Int              | 主键                 | R    |
| internal_name   | String           | 登录名称             | RW   |
| password        | String           | 密码                 | W    |
| is_active       | Boolean          | 是否可用             | RW   |
| role            | user_role_choice | 角色选项             | RW   |
| is_staff        | Boolean          | 具备管理权限         | RW   |
| registered_date | datetime         | 注册日期             | R    |
| pn              | String           | 手机号               | RW   |
| last_login      | datetime         | 上次登录             | RW   |
| user_validate   | UserValidateView | 用户实名认证信息视图 | RW   |

