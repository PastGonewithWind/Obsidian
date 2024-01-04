es服务器端访问

```shell
curl --user '[admin]':'[pwd]' [ip]/[port]
```

es服务器端查询

```shell
curl --user '[admin]':'[pwd]' [ip]/[port]/[index]/_search
```

es索引创建
```
put http://109.101.105.171:8002/ngs2-sit-chat、ngs2-prod-chat

{
    "mappings": {
        "properties": {
            "content": {
                "type": "text",
                "analyzer": "ik_max_word"
            },
            "user_id": {
                "type": "keyword"
            },
            "title": {
                "type": "keyword"
            }
        }
    }
}
```

