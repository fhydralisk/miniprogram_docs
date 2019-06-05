# QcPlace端相关视图

### QcPlaceView

质检场地视图

| 字段名称    | 类型           | 含义               | 读写 |
| ----------- | -------------- | ------------------ | ---- |
| id          | Int            | 质检场地ID         | QW   |
| lat         | Decimal        | 纬度               | RW   |
| lng         | Decimal        | 经度               | RW   |
| name        | String         | 姓名               | RW   |
| loc_desc    | Text           | 地点描述           | RW   |
| in_use      | Boolean        | 是否在使用         | RW   |
| create_time | Timestamp      | 添加时间           | R    |
| admins      | List of String | 场地管理员姓名列表 | R    |

