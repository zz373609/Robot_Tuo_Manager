# 数据库设计

## 数据库

使用 Mongo 4。

## 结构

### 用户

collection: `user`

| 字段         | 类型                      | 名称     | 说明                               |
| ------------ | ------------------------- | -------- | ---------------------------------- |
| `_id`        | string                    | 用户 ID  | 主键                               |
| `wechat_id`  | string                    | 微信 ID  | unique index                       |
| `level`      | [Level](#level)           | 会员级别 |                                    |
| `footprint`  | [Footprint](#footprint)[] | 足迹     |                                    |
| `tags`       | [Tag](#tag)[]             | 标签     |                                    |
| `state`      | string                    | 状态     | ( inactive \| active \| forbidden) |
| `created_at` | number                    | 创建日期 | UNIX 时间戳                        |

PS: [微信小程序用户信息 API](https://developers.weixin.qq.com/miniprogram/dev/api/UserInfo.html)

#### objects

##### Tag

| 字段   | 类型   | 名称   | 说明 |
| ------ | ------ | ------ | ---- |
| `name` | string | 标签名 |      |
| `code` | string | 激活码 |      |

##### Level

| 字段    | 类型   | 名称     | 说明 |
| ------- | ------ | -------- | ---- |
| `name`  | string | 级别名称 |      |
| `price` | number | 定价     |      |

##### Footprint

| 字段         | 类型   | 名称         | 说明        |
| ------------ | ------ | ------------ | ----------- |
| `place`      | string | 景点名       |             |
| `created_at` | number | 景点到达日期 | UNIX 时间戳 |

### 用户录音记录

collection: `audio`

| 字段         | 类型   | 名称           | 说明        |
| ------------ | ------ | -------------- | ----------- |
| `_id`        | string | 录音 ID        | 主键        |
| `wechat_id`  | string | 用户 ID        | user 表外键 |
| `data`       | buffer | 音频二进制文件 |             |
| `text`       | string | 转换文本       |             |
| `created_at` | number | 创建日期       | UNIX 时间戳 |

### 景点位置

collection: `location`

| 字段   | 类型   | 名称   | 说明 |
| ------ | ------ | ------ | ---- |
| `_id`  | string | ID     | 主键 |
| `name` | string | 景点名 |      |
| `long` | number | 经度   |      |
| `lat`  | number | 纬度   |      |

### 事件

collection: `event`

| 字段         | 类型              | 名称     | 说明 |
| ------------ | ----------------- | -------- | ---- |
| `_id`        | string            | ID       | 主键 |
| `key`        | string            | 事件类型 |      |
| `desc`       | string            | 事件描述 |      |
| `audio`      | [Audio](#audio)[] | 语音列表 |      |
| `created_at` | string            | 创建时间 |      |

#### objects

##### Audio

| 字段   | 类型   | 名称     | 说明 |
| ------ | ------ | -------- | ---- |
| `text` | string | 语音文本 |      |
| `link` | string | 语音链接 |      |

### 激活码

collection: `activation`

| 字段         | 类型   | 名称         | 说明                 |
| ------------ | ------ | ------------ | -------------------- |
| `_id`        | string | ID           | 主键                 |
| `code`       | string | 激活码       |                      |
| `kind`       | string | 类型         |                      |
| `name`       | string | 名称         |                      |
| `wechat_id`  | string | 绑定微信用户 | 若为空，代表没使用过 |
| `created_at` | number | 创建时间     |                      |
| `expired_at` | number | 过期时间     |                      |
| `used_at`    | number | 使用时间     |                      |
