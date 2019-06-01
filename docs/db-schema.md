# 数据库设计

| 版本号 | 修订说明     | 修订人    | 修订时间   |
| ------ | ------------ | --------- | ---------- |
| 0.1.3  | 字段更新 | minazukie | 2019/06/01 |
| 0.1.2  | 渠道字段更新 | minazukie | 2019/05/25 |
| 0.1.1  | 渠道字段更新 | minazukie | 2019/05/15 |
| 0.1.0  | 第一版       | minazukie | 2019/05/14 |

## 数据库

使用 Mongo 4。

## 结构

### 用户

collection: `user`

| 字段              | 类型                          | 名称         | 说明                               |
| ----------------- | ----------------------------- | ------------ | ---------------------------------- |
| `_id`             | string                        | 用户 ID      | 主键                               |
| `wechat_id`       | string                        | 微信 ID      | unique index                       |
| `youzan_id`       | string                        | 有赞 ID      | unique index                       |
| `nickname`        | string                        | 昵称         |                                    |
| `gender`          | number                        | 性别         | 0 未知，1 男性，2 女性             |
| `country`         | string                        | 国家         |                                    |
| `province`        | string                        | 省份         |                                    |
| `city`            | string                        | 城市         |                                    |
| `language`        | string                        | 语言         |                                    |
| `activation_code` | string                        | 激活码       |                                    |
| `level`           | [Level](#level)               | 会员级别     |                                    |
| `achievement`     | [Achievement](#achievement)[] | 成就         |                                    |
| `from_type`       | [fromType](#fromType)         | 渠道         |                                    |
| `state`           | string                        | 状态         | ( inactive \| active \| forbidden) |
| `created_at`      | number                        | 创建日期     | UNIX 时间戳                        |
| `updated_at`      | number                        | 上次更新日期 | UNIX 时间戳                        |
| `deleted_at`      | number                        | 删除日期     | UNIX 时间戳                        |

PS: [微信小程序用户信息 API](https://developers.weixin.qq.com/miniprogram/dev/api/UserInfo.html)

#### objects

##### FromType

| 字段   | 类型   | 名称     | 说明 |
| ------ | ------ | -------- | ---- |
| `kind` | string | 渠道类型 |      |
| `name` | string | 名称     |      |

##### Level

| 字段    | 类型   | 名称     | 说明 |
| ------- | ------ | -------- | ---- |
| `name`  | string | 级别名称 |      |
| `price` | number | 定价     |      |

##### Achievement

| 字段         | 类型   | 名称         | 说明        |
| ------------ | ------ | ------------ | ----------- |
| `name`       | string | 成就名称     |             |
| `created_at` | number | 成就达成日期 | UNIX 时间戳 |

### 用户录音记录

collection: `audio`

| 字段         | 类型   | 名称           | 说明        |
| ------------ | ------ | -------------- | ----------- |
| `_id`        | string | 录音 ID        | 主键        |
| `user_id`    | string | 用户 ID        | user 表外键 |
| `data`       | buffer | 音频二进制文件 |             |
| `text`       | string | 转换文本       |             |
| `created_at` | number | 创建日期       | UNIX 时间戳 |

### 景点

collection: `spot`

| 字段        | 类型   | 名称   | 说明 |
| ----------- | ------ | ------ | ---- |
| `_id`       | number | ID     | 主键 |
| `name`      | string | 景点名 |      |
| `longitude` | number | 经度   |      |
| `latitude`  | number | 纬度   |      |
