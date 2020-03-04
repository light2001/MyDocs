### Elasticsearch增删改查演练


#### 下面是测试语句
~~~

-- 查询所有
GET /grapes/product/_search

-- 新增
PUT /grapes/product/2
{
    "name" : "黑玫瑰",
    "desc" :  "黑玫瑰",
    "price" :  25,
    "producer" :      "jiajieshi producer1",
    "tags": [ "fangzhu1" ]
}

-- 新增
PUT /grapes/product/3
{
    "name" : "黑玫瑰",
    "desc" :  "黑玫瑰",
    "price" :  25,
    "producer" :      "jiajieshi producer1",
    "tags": [ "fangzhu1" ]
}

-- 更新单条数据
POST /grapes/product/2/_update
{
   "doc":{
     "name" : "黑玫瑰1",
     "desc" : "黑玫瑰2"
   }
}

-- 查询/grapes/product下所有数据
GET /grapes/product/_search
{
  "query": {
    "match": {
      "name": "夏黑"
    }},
  "sort": [
    {
      "price": {
        "order": "asc"
      }
    }
  ],
  "_source": ["name","price"]
}

-- 删除数据
DELETE /grapes/product/3

-- 组合查询
GET /grapes/product/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
          "name": "夏"
        }}
      ], 
      "filter": {
        "range": {
          "price": {
            "gt": 24
          }
        }
      }
    }
  }
}

-- 匹配查询
GET /grapes/product/_search
{
  "query": {
    "match_phrase": {
      "name": "夏黑"
    }
  }
}

~~~