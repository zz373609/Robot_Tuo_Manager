# 数据库设计

## 数据库

使用 Mongo 4。

## 结构

### 用户

collection: `user`

| 字段         | 类型          | 名称     | 说明                               |
| ------------ | ------------- | -------- | ---------------------------------- |
| `_id`        | str           | 用户 ID  | 主键                               |
| `wechat_id`  | str           | 微信 ID  | unique index                       |
| `level`      | str           | 会员级别 |                                    |
| `tags`       | [Tag](#tag)[] | 标签     |                                    |
| `state`      | str           | 状态     | ( inactive \| active \| forbidden) |
| `created_at` | int           | 创建日期 | UNIX 时间戳                        |

PS: [微信小程序用户信息 API](https://developers.weixin.qq.com/miniprogram/dev/api/UserInfo.html)

#### objects

##### Tag

| 字段     | 类型 | 名称   | 说明                        |
| -------- | ---- | ------ | --------------------------- |
| `name`   | str  | 标签名 |                             |
| `code`   | str  | 激活码 |                             |
| `source` | str  | 来源   | activation_code, wechat_pay |

### 足迹

collection: `footprint`

| 字段         | 类型 | 名称         | 说明        |
| ------------ | ---- | ------------ | ----------- |
| `_id`        | str  | ID           | 主键        |
| `wechat_id`  | str  | 用户 ID      |             |
| `place`      | str  | 景点名       |             |
| `created_at` | int  | 景点到达日期 | UNIX 时间戳 |

### 优惠券

collection: `coupon`

| 字段                | 类型 | 名称           | 说明        |
| ------------------- | ---- | -------------- | ----------- |
| `_id`               | str  | ID             | 主键        |
| `wechat_id`         | str  | 用户 ID        |             |
| `name`              | str  | 优惠券名称     |             |
| `code`              | str  | 优惠码         |             |
| `intro_type`        | str  | 介绍类型       |             |
| `intro_url`         | str  | 图片或视频 URL |             |
| `merchant`          | str  | 商家名称       |             |
| `merchant_location` | str  | 商家位置       |             |
| `price`             | int  | 价格           | 单位：分    |
| `used`              | bool | 是否使用过     |             |
| `created_at`        | int  | 添加时间       | UNIX 时间戳 |
| `used_at`           | int  | 使用时间       | UNIX 时间戳 |

### 用户录音记录

collection: `audio`

| 字段         | 类型  | 名称           | 说明        |
| ------------ | ----- | -------------- | ----------- |
| `_id`        | str   | 录音 ID        | 主键        |
| `wechat_id`  | str   | 用户 ID        | user 表外键 |
| `data`       | bytes | 音频二进制文件 |             |
| `text`       | str   | 转换文本       |             |
| `created_at` | int   | 创建日期       | UNIX 时间戳 |

### 景点位置

collection: `location`

| 字段   | 类型  | 名称   | 说明 |
| ------ | ----- | ------ | ---- |
| `_id`  | str   | ID     | 主键 |
| `name` | str   | 景点名 |      |
| `long` | float | 经度   |      |
| `lat`  | float | 纬度   |      |

### 事件

collection: `event`

| 字段         | 类型              | 名称     | 说明 |
| ------------ | ----------------- | -------- | ---- |
| `_id`        | str               | ID       | 主键 |
| `key`        | str               | 事件类型 |      |
| `desc`       | str               | 事件描述 |      |
| `audio`      | [Audio](#audio)[] | 语音列表 |      |
| `created_at` | str               | 创建时间 |      |

#### objects

##### Audio

| 字段   | 类型 | 名称     | 说明 |
| ------ | ---- | -------- | ---- |
| `text` | str  | 语音文本 |      |
| `link` | str  | 语音链接 |      |

### 激活码

collection: `activation`

| 字段         | 类型 | 名称         | 说明                 |
| ------------ | ---- | ------------ | -------------------- |
| `_id`        | str  | ID           | 主键                 |
| `code`       | str  | 激活码       |                      |
| `kind`       | str  | 类型         |                      |
| `name`       | str  | 名称         |                      |
| `wechat_id`  | str  | 绑定微信用户 | 若为空，代表没使用过 |
| `created_at` | int  | 创建时间     |                      |
| `expired_at` | int  | 过期时间     |                      |
| `used_at`    | int  | 使用时间     |                      |

### 商品

collection: `good`

| 字段         | 类型 | 名称     | 说明     |
| ------------ | ---- | -------- | -------- |
| `_id`        | str  | ID       | 主键     |
| `kind`       | str  | 类型     |          |
| `name`       | str  | 名称     |          |
| `price`      | int  | 价格     | 单位：分 |
| `created_at` | int  | 创建时间 |          |

### 订单

collection: `order`

| 字段           | 类型 | 名称       | 说明 |
| -------------- | ---- | ---------- | ---- |
| `_id`          | str  | ID         | 主键 |
| `out_trade_no` | str  | 内部订单号 |      |
| `wechat_id`    | str  | 用户 ID    |      |
| `good_id`      | str  | 商品 ID    |      |
| `state`        | str  | 订单状态   |      |
| `created_at`   | int  | 创建时间   |      |
