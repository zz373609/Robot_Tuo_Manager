# 机器人对话

## 语音识别文字

```
POST /robot/talk
```

| 属性       | 位置      | 类型 | 是否必填 | 描述                                               |
| ---------- | --------- | ---- | -------- | -------------------------------------------------- |
| `wechat_id` | form-data | str  | yes       | 微信用户ID |
| `file`     | form-data | file | yes      | 音频文件                                           |
| `provider` | form-data | str  | no       | 语音识别提供者(默认ths)。可选择:ths, xunfei, baidu |

响应数据：

```json
{
  "text": "示例文字"
}
```

## 问答

```
POST /robot/ask
```

| 属性        | 位置 | 类型 | 是否必填 | 描述                                        |
| ----------- | ---- | ---- | -------- | ------------------------------------------- |
| `wechat_id` | body | str  | yes      | 微信用户ID                                  |
| `question`  | body | str  | yes      | 问题                                        |
| `robot`     | body | str  | no       | 机器人(默认ths)。可选择:ths, baidu          |
| `provider`  | body | str  | no       | 语音合成提供者(默认ths)。可选择:ths, xunfei |

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
    "lat": 45.00,
    "long": 45.00
  }
}
```

