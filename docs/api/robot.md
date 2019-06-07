# 机器人对话

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
  "touch_head": {
    "desc": "摸头",
    "audio": [
      {
        "text": "你好你好",
        "link": "https://"
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

响应数据：

```json
{
  "footprint": [
    {
      "place": "太阳广场",
      "created_at": 1234567890
    },
    {
      "place": "月亮广场",
      "created_at": 1234567890
    }
  ]
}
```

## 添加用户足迹

```
POST /user/:wechat_id/footprint
```

| 属性    | 位置 | 类型   | 是否必填 | 描述     |
| ------- | ---- | ------ | -------- | -------- |
| `place` | data | string | 是       | 地点名称 |

响应数据：

```json
{
  "place": "太阳广场",
  "created_at": 1234567890
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
      "used": false,
      "created_at": 1234567890,
      "used_at": 0
    },
    {
      "wechat_id": "xxx",
      "name": "zzz",
      "code": "def",
      "used": true,
      "created_at": 1234567890,
      "used_at": 1234567890
    }
  ]
}
```

## 添加用户优惠券

```
POST /user/:wechat_id/coupon
```

| 属性   | 位置 | 类型   | 是否必填 | 描述       |
| ------ | ---- | ------ | -------- | ---------- |
| `name` | data | string | 是       | 优惠券名称 |

响应数据：

```json
{
  "wechat_id": "xxx",
  "name": "yyy",
  "code": "abc",
  "used": false,
  "created_at": 1234567890,
  "used_at": 0
}
```
