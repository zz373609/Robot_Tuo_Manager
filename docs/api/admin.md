# 后台

- [后台](#%E5%90%8E%E5%8F%B0)
  - [用户信息](#%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF)

## 用户信息

```
GET /admin/user
```

| 属性         | 位置  | 类型    | 是否必填 | 描述                                          |
| ------------ | ----- | ------- | -------- | --------------------------------------------- |
| `page`       | query | integer | 否       | 页码，默认 1                                  |
| `page_size`  | query | integer | 否       | 每页数量，默认 20                             |
| `order_by`   | query | str     | 否       | 排序依据，默认 created_at                     |
| `asc`        | query | str     | 否       | 是否升序（若为空则降序，不为空则升序）        |
| `tag`        | query | string  | 否       | 会员类别名称，默认「天河潭会员」              |
| `start_time` | query | integer | 否       | 开始时间，默认-1                              |
| `end_time`   | query | integer | 否       | 结束时间，默认-1                              |
| `export`     | query | string  | 否       | 是否导出信息（若为空则 false，不为空则 true） |

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
