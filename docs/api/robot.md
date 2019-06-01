# 机器人对话

## 语音识别文字

```
POST /robot/talk
```

| 属性       | 位置      | 类型 | 是否必填 | 描述                                               |
| ---------- | --------- | ---- | -------- | -------------------------------------------------- |
| `file`     | form-data | file | yes      | 音频文件                                           |
| `provider` | form-data | str  | no       | 语音识别提供者(默认ths)。可选择:ths, baidu, xunfei |

响应数据：

```json
{
  "text": "示例文字"
}
```

## 问答

```
GET /robot/ask
```

| 属性       | 位置 | 类型 | 是否必填 | 描述                                               |
| ---------- | ---- | ---- | -------- | -------------------------------------------------- |
| `question` | body | str  | yes      | 音频文件                                           |
| `robot`    | body | str  | no       | 机器人(默认ths)。可选择:ths, baidu, xunfei         |
| `provider` | body | str  | no       | 语音合成提供者(默认ths)。可选择:ths, baidu, xunfei |

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
    "lat": 45.00,
    "long": 45.00
  }
}
```

