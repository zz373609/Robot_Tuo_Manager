# 机器人对话

- [机器人对话](#%E6%9C%BA%E5%99%A8%E4%BA%BA%E5%AF%B9%E8%AF%9D)
  - [语音识别文字](#%E8%AF%AD%E9%9F%B3%E8%AF%86%E5%88%AB%E6%96%87%E5%AD%97)
  - [文字合成语音](#%E6%96%87%E5%AD%97%E5%90%88%E6%88%90%E8%AF%AD%E9%9F%B3)
  - [问答](#%E9%97%AE%E7%AD%94)
  - [事件语音](#%E4%BA%8B%E4%BB%B6%E8%AF%AD%E9%9F%B3)
  - [注册用户](#%E6%B3%A8%E5%86%8C%E7%94%A8%E6%88%B7)
  - [查看用户足迹](#%E6%9F%A5%E7%9C%8B%E7%94%A8%E6%88%B7%E8%B6%B3%E8%BF%B9)
  - [添加用户足迹](#%E6%B7%BB%E5%8A%A0%E7%94%A8%E6%88%B7%E8%B6%B3%E8%BF%B9)
  - [查看用户优惠券](#%E6%9F%A5%E7%9C%8B%E7%94%A8%E6%88%B7%E4%BC%98%E6%83%A0%E5%88%B8)
  - [添加用户优惠券](#%E6%B7%BB%E5%8A%A0%E7%94%A8%E6%88%B7%E4%BC%98%E6%83%A0%E5%88%B8)
  - [使用用户优惠券](#%E4%BD%BF%E7%94%A8%E7%94%A8%E6%88%B7%E4%BC%98%E6%83%A0%E5%88%B8)
  - [获取景点位置信息](#%E8%8E%B7%E5%8F%96%E6%99%AF%E7%82%B9%E4%BD%8D%E7%BD%AE%E4%BF%A1%E6%81%AF)
  - [支付](#%E6%94%AF%E4%BB%98)

## 语音识别文字

```
POST /robot/talk
```

| 属性        | 位置      | 类型   | 是否必填 | 描述                                                |
| ----------- | --------- | ------ | -------- | --------------------------------------------------- |
| `wechat_id` | form-data | string | 是       | 微信用户 ID                                         |
| `file`      | form-data | file   | 是       | 音频文件                                            |
| `provider`  | form-data | string | 否       | 语音识别提供者(默认 ths)。可选择:ths, xunfei, baidu |

响应数据：

```json
{
  "text": "示例文字"
}
```

## 文字合成语音

```
POST /robot/to_audio
```

| 属性       | 位置 | 类型     | 是否必填 | 描述                                                |
| ---------- | ---- | -------- | -------- | --------------------------------------------------- |
| `texts`    | data | string[] | 是       | 文字                                                |
| `provider` | data | string   | 否       | 语音识别提供者(默认 ths)。可选择:ths, xunfei, baidu |
| `voice`    | data | string   | 否       | 朗诵人(当前仅讯飞可用，默认 xiaoyan)                |

响应数据：

```json
{
  "text": "你好",
  "link": "https://"
}
```

## 问答

```
POST /robot/ask
```

| 属性         | 位置 | 类型   | 是否必填 | 描述                                         |
| ------------ | ---- | ------ | -------- | -------------------------------------------- |
| `wechat_id`  | body | string | 是       | 微信用户 ID                                  |
| `question`   | body | string | 是       | 问题                                         |
| `robot`      | body | string | 否       | 机器人(默认 ths)。可选择:ths, baidu          |
| `provider`   | body | string | 否       | 语音合成提供者(默认 ths)。可选择:ths, xunfei |
| `session_id` | body | string | 是       | 会话 ID                                      |

问答协议：

答案分为 text、image、video 三种类型，不同类型之间的数据使用---[数据类型]---数据---/[数据类型]---包住，同种类型之间的数据使用-----分割，注意数据内不能有-----。例如：

```
---text---哈哈哈你好-----嘻嘻嘻我不好---/text------image---https://xxxxxxxx---/image---
```

响应数据：

```json
{
  "texts": [
    {
      "content": "文本内容",
      "link": "https://"
    }
  ],
  "images": [
    {
      "content": "图片内容",
      "link": "https://"
    }
  ],
  "videos": [
    {
      "content": "视频内容",
      "link": "https://"
    }
  ],
  "location": {
    "name": "天河潭",
    "valid": true,
    "lat": 45.0,
    "long": 45.0
  },
  "session_id": "xxx"
}
```

## 事件语音

```
GET /event
```

响应数据：

key 是事件类型。

```json
{
  "location": {
    "valid": true,
    "name": "太阳广场",
    "text": "你好你现在在太阳广场",
    "link": "https://"
  },
  "touch_head": {
    "desc": "摸头",
    "audio": [
      {
        "text": "你好你好",
        "link": "https://"
      }
    ],
    "text": [
      {
        "text": "xxx"
      }
    ]
  },
  "touch_body": {
    "desc": "摸身体",
    "audio": [
      {
        "text": "娃哈哈哈",
        "link": "https://"
      }
    ],
    "text": [
      {
        "text": "xxx"
      }
    ]
  },
  "welcome_text": {
    "desc": "欢迎语",
    "audio": [],
    "text": [
      {
        "text": "xxx"
      }
    ]
  }
}
```

## 注册用户

```
POST /user
```

| 属性              | 位置 | 类型   | 是否必填 | 描述         |
| ----------------- | ---- | ------ | -------- | ------------ |
| `wechat_code`     | data | string | 是       | 微信 js_code |
| `activation_code` | data | string | 否       | 激活码       |

响应数据：

```json
{
  "is_new": true,
  "user": {
    "id": "xxx",
    "wechat_id": "yyy",
    "tags": [],
    "level": "普通会员",
    "state": "active",
    "created_at": 123456890
  }
}
```

## 查看用户足迹

```
GET /user/:wechat_id/footprint
```

该接口会返回所有的主要景点，played 代表是否已经来过。

响应数据：

```json
{
  "footprint": [
    {
      "place": "太阳广场",
      "lat": "26.444836",
      "long": "106.581438",
      "is_main": true,
      "played": true,
      "created_at": 1234567890
    },
    {
      "place": "月亮广场",
      "lat": "26.444836",
      "long": "106.581438",
      "is_main": true,
      "played": false,
      "created_at": 1234567890
    }
  ]
}
```

## 添加用户足迹

```
POST /user/:wechat_id/footprint
```

| 属性   | 位置 | 类型   | 是否必填 | 描述 |
| ------ | ---- | ------ | -------- | ---- |
| `lat`  | data | number | 是       | 纬度 |
| `long` | data | number | 是       | 经度 |

响应数据：

```json
{
  "valid_place": true,
  "welcome_audio": {
    "text": "你在太阳广场",
    "link": "https://"
  },
  "current_place": {
    "first_time": true,
    "place": "太阳广场",
    "lat": "26.444836",
    "long": "106.581438",
    "is_main": true,
    "created_at": 1234567890
  }
}
```

## 查看用户优惠券

```
GET /user/:wechat_id/coupon
```

响应数据：

```json
{
  "coupon": [
    {
      "wechat_id": "xxx",
      "name": "yyy",
      "code": "abc",
      "image_url": "https://",
      "video_url": "https://",
      "video_type": "gif",
      "lat": 26.446445,
      "long": 26.446445,
      "used": false,
      "merchant": "商家",
      "merchant_location": "太阳广场",
      "price": 700,
      "created_at": 1234567890,
      "used_at": 0
    }
  ]
}
```

## 添加用户优惠券

```
POST /user/:wechat_id/coupon
```

| 属性                | 位置 | 类型   | 是否必填 | 描述                 |
| ------------------- | ---- | ------ | -------- | -------------------- |
| `name`              | data | string | 是       | 优惠券名称           |
| `spot`              | data | string | 是       | 景区                 |
| `merchant`          | data | string | 是       | 商家                 |
| `merchant_location` | data | string | 是       | 商家位置             |
| `merchant_lat`      | data | string | 是       | 商家纬度             |
| `merchant_long`     | data | string | 是       | 商家经度             |
| `price`             | data | number | 是       | 价格（单位：分）     |
| `image_url`         | data | number | 是       | 图片地址             |
| `video_url`         | data | number | 是       | 视频地址             |
| `video_type`        | data | number | 是       | 视频类型(gif, video) |

响应数据：

```json
{
  "wechat_id": "xxx",
  "spot": "天河潭",
  "name": "yyy",
  "code": "abc",
  "image_url": "https://",
  "video_url": "https://",
  "video_type": "gif",
  "used": false,
  "merchant": "商家",
  "merchant_location": "太阳广场",
  "merchant_lat": 123.111,
  "merchant_long": 9.9999,
  "price": 700,
  "created_at": 1234567890,
  "used_at": 0
}
```

## 使用用户优惠券

```
POST /user/:wechat_id/coupon/:coupon_id/use
```

响应数据：

```json
{
  "wechat_id": "xxx",
  "spot": "天河潭",
  "name": "yyy",
  "code": "abc",
  "image_url": "https://",
  "video_url": "https://",
  "video_type": "gif",
  "used": true,
  "merchant": "商家",
  "merchant_location": "太阳广场",
  "price": 700,
  "created_at": 1234567890,
  "used_at": 1234567890
}
```

## 获取景点位置信息

```
GET /location
```

响应数据：

```json
{
  "location": [
    {
      "name": "风雨桥",
      "lat": 26.446445,
      "long": 106.580628,
      "id": "5cf2af19278e4e14a18f756f"
    },
    {
      "name": "灵动水景",
      "lat": 26.446118,
      "long": 106.580772,
      "id": "5cf2af19278e4e14a18f7570"
    }
  ]
}
```

## 支付

```
POST /pay
```

| 属性        | 位置 | 类型   | 是否必填 | 描述    |
| ----------- | ---- | ------ | -------- | ------- |
| `wechat_id` | data | string | 是       | 用户 ID |
| `good_id`   | data | string | 是       | 商品 ID |

响应数据：

```json
{
  "appId": "app_id",
  "nonceStr": "nonce_str",
  "package": "package",
  "sign": "sign",
  "signType": "MD5",
  "timeStamp": "timestamp"
}
```
