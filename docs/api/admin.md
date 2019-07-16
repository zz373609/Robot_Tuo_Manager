# 后台

- [后台](#%E5%90%8E%E5%8F%B0)
  - [权限认证](#%E6%9D%83%E9%99%90%E8%AE%A4%E8%AF%81)
  - [用户信息](#%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF)
  - [景区热度](#%E6%99%AF%E5%8C%BA%E7%83%AD%E5%BA%A6)
  - [问答记录](#%E9%97%AE%E7%AD%94%E8%AE%B0%E5%BD%95)

## 权限认证

```
POST /auth
```

| 属性       | 位置 | 类型   | 是否必填 | 描述                      |
| ---------- | ---- | ------ | -------- | ------------------------- |
| `username` | body | String | 是       | 用户名                    |
| `password` | body | String | 是       | 密码（使用 MD5 掩盖明文） |

响应数据：

```json
{
  "access_token": "xxxxxxxxxxxxxxxx"
}
```

请求有权限要求的接口，需要在 header 添加以下键值对：

```
Authorization: JWT xxxxxxxxxxxxxxxx
```

## 用户信息

```
GET /admin/user
```

| 属性         | 位置  | 类型    | 是否必填 | 描述                                                     |
| ------------ | ----- | ------- | -------- | -------------------------------------------------------- |
| `page`       | query | integer | 否       | 页码，默认 1                                             |
| `page_size`  | query | integer | 否       | 每页数量，默认 20                                        |
| `order_by`   | query | string  | 否       | 排序依据，默认 created_at                                |
| `asc`        | query | string  | 否       | 是否升序（若为空则降序，不为空则升序）                   |
| `tag`        | query | string  | 否       | 会员类别名称，默认「天河潭会员」                         |
| `start_time` | query | integer | 否       | 开始时间，默认-1（格式是 10 位时间戳，例如：1562755473） |
| `end_time`   | query | integer | 否       | 结束时间，默认-1（格式是 10 位时间戳，例如：1562755473） |
| `export`     | query | string  | 否       | 是否导出信息（若为空则 false，不为空则 true）            |

响应数据：

```json
{
  "page": 1,
  "pages": 51,
  "count_per_page": 20,
  "total": 1013,
  "users": [
    {
      "wechat_id": "o-N645YJ52PmSdN3jqOwZFZcGZJw",
      "level": "normal",
      "state": "active",
      "created_at": 1562755451,
      "id": "5d25c17b1d4e9bf81327379e",
      "tag": {
        "name": "天河潭会员",
        "source": "wechat_pay",
        "code": "VxyTdzqwdagzBpHbtD1TGtv73Rzi1Uyd",
        "created_at": 1562755473
      },
      "footprint_count": 0
    }
  ]
}
```

## 景区热度

```
GET /admin/hot_spot
```

| 属性         | 位置  | 类型    | 是否必填 | 描述                                                     |
| ------------ | ----- | ------- | -------- | -------------------------------------------------------- |
| `start_time` | query | integer | 否       | 开始时间，默认-1（格式是 10 位时间戳，例如：1562755473） |
| `end_time`   | query | integer | 否       | 结束时间，默认-1（格式是 10 位时间戳，例如：1562755473） |

响应数据：

```json
{
  "spots": [
    {
      "_id": "风雨桥",
      "total": 1
    },
    {
      "_id": "同心台",
      "total": 1
    },
    {
      "_id": "游客服务中心",
      "total": 1
    },
    {
      "_id": "太阳广场",
      "total": 1
    },
    {
      "_id": "银河宫（旱溶洞）",
      "total": 1
    }
  ]
}
```

## 问答记录

```
GET /admin/audio
```

| 属性         | 位置  | 类型    | 是否必填 | 描述                                                     |
| ------------ | ----- | ------- | -------- | -------------------------------------------------------- |
| `page`       | query | integer | 否       | 页码，默认 1                                             |
| `page_size`  | query | integer | 否       | 每页数量，默认 20                                        |
| `order_by`   | query | string  | 否       | 排序依据，默认 created_at                                |
| `asc`        | query | string  | 否       | 是否升序（若为空则降序，不为空则升序）                   |
| `wechat_id`  | query | string  | 否       | 微信 ID                                                  |
| `question`   | query | string  | 否       | 问题                                                     |
| `start_time` | query | integer | 否       | 开始时间，默认-1（格式是 10 位时间戳，例如：1562755473） |
| `end_time`   | query | integer | 否       | 结束时间，默认-1（格式是 10 位时间戳，例如：1562755473） |
| `export`     | query | string  | 否       | 是否导出信息（若为空则 false，不为空则 true）            |

响应数据：

```json
{
  "page": 1,
  "pages": 1,
  "count_per_page": 20,
  "total": 7,
  "audio": [
    {
      "wechat_id": "aa",
      "question": "风雨桥",
      "answer": {
        "texts": [
          {
            "content": "提到风雨桥，孃孃得说道说道了，它可是侗族建筑三宝之一。桥上印着神兽祥云图纹。据说这个图案可以镇邪和留住财银；在风雨桥上走，能祈愿未来前途更精彩，生活更加美好，感情更加牢固。它前面就是星月楼牌，可以来问我它的故事",
            "link": "http://static.yubuqianxing.com/media/01x_mengmenghappy-b6501ddc094d0989e68e2dae48b6560d.wav"
          }
        ],
        "images": [],
        "videos": [],
        "location": {
          "valid": true,
          "name": "风雨桥",
          "lat": 26.446445,
          "long": 106.580628,
          "keywords": ["风雨桥"],
          "goto": false
        },
        "session_id": "service-session-id-1561994604108-68630e85c38345309fe475715db2639e"
      },
      "provider": "xunfei",
      "created_at": 1561994604,
      "id": "5d1a256c77bbd8aabe28cb5c",
      "answer_type": "has_answer"
    }
  ]
}
```

answer_type：

"has_answer" 有答案

"no_answer" 无答案兜底

"no_record" 无录音兜底

"" 无记录
