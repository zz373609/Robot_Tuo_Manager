# 数据库设计

| 版本号 | 修订说明 | 修订人    | 修订时间   |
| ------ | -------- | --------- | ---------- |
| 0.1.0  | 第一版   | minazukie | 2019/05/14 |

## 数据库

使用 Mongo 4。

## 结构

### 用户

collection: `user`

| 字段             | 类型                          | 名称         | 说明                               |
| ---------------- | ----------------------------- | ------------ | ---------------------------------- |
| `_id`            | number                        | 用户 ID      | 主键                               |
| `wechatId`       | string                        | 微信 ID      | unique index                       |
| `youzanId`       | string                        | 有赞 ID      | unique index                       |
| `nickName`       | string                        | 昵称         |                                    |
| `gender`         | number                        | 性别         | 0 未知，1 男性，2 女性             |
| `country`        | string                        | 国家         |                                    |
| `province`       | string                        | 省份         |                                    |
| `city`           | string                        | 城市         |                                    |
| `language`       | string                        | 语言         |                                    |
| `activationCode` | string                        | 激活码       |                                    |
| `level`          | [Level](#level)               | 会员级别     |                                    |
| `achievement`    | [Achievement](#achievement)[] | 成就         |                                    |
| `state`          | string                        | 状态         | ( inactive \| active \| forbidden) |
| `createdAt`      | number                        | 创建日期     | UNIX 时间戳                        |
| `updatedAt`      | number                        | 上次更新日期 | UNIX 时间戳                        |
| `deletedAt`      | number                        | 删除日期     | UNIX 时间戳                        |

PS: [微信小程序用户信息 API](https://developers.weixin.qq.com/miniprogram/dev/api/UserInfo.html)

#### objects

##### Level

| 字段    | 类型   | 名称     | 说明 |
| ------- | ------ | -------- | ---- |
| `name`  | string | 级别名称 |      |
| `price` | number | 定价     |      |

##### Achievement

| 字段        | 类型   | 名称         | 说明        |
| ----------- | ------ | ------------ | ----------- |
| `name`      | string | 成就名称     |             |
| `createdAt` | number | 成就达成日期 | UNIX 时间戳 |

### 用户录音记录

collection: `audio`

| 字段        | 类型   | 名称           | 说明        |
| ----------- | ------ | -------------- | ----------- |
| `_id`       | number | 录音 ID        | 主键        |
| `userId`    | string | 用户 ID        | user 表外键 |
| `data`      | buffer | 音频二进制文件 |             |
| `text`      | string | 转换文本       |             |
| `createdAt` | number | 创建日期       | UNIX 时间戳 |
