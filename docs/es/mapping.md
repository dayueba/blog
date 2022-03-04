字段的映射包括但不限于
- 字段的数据类型
- 是否要存储
- 是否要索引
- 分词器
> 文档地址：https://www.elastic.co/guide/en/elasticsearch/reference/7.3/mapping-params.html

## 创建映射字段
语法
```
PUT /索引库名/_mapping
{
  "properties": {
    "字段名": {
      "type": "类型",
      "index": true，
      "store": true，
      "analyzer": "分词器"
    }
  }
}
```
说明：
- type：类型，可以是text、long、short、date、integer、object等
- index：是否索引，默认为true
- store：是否存储，默认为false
- analyzer：指定分词器

例子
```
PUT /company-index/_mapping/
{
  "properties": {
    "name": {
      "type": "text",
      "analyzer": "ik_max_word"
    },
    "job": {
      "type": "text",
      "analyzer": "ik_max_word"
    },
    "logo": {
      "type": "keyword",
      "index": "false"
    },
    "payment": {
      "type": "float"
    }
  }
}
```
### type
> 文档：https://www.elastic.co/guide/en/elasticsearch/reference/7.3/mapping-types.html

重点：
- string
    - text：可分词 不可参与聚合
    - keyword：不可参与分词 数据会作为完整字段进行匹配 可以参与聚合
- Numerical：数值类型
    - 基本数据类型：long, integer, short, byte, double, float, half_float
    - 浮点数的高精度类型：scaled_float
        - 需要指定一个精度因子，比如10或100。elasticsearch会把真实值乘以这个因子后存储，取出时再复原。
- Date：日期类型
- Array
    - 进行匹配时，任意一个元素满足，都认为满足
    - 排序时，如果升序则用数组中的最小值来排序，如果降序则用数组中的最大值来排序
- Object
    - 如果存储到索引库的是对象类型，例如上面的girl，会把girl变成两个字段：girl.name和girl.age

### index
index影响字段的索引情况。
- true：字段会被索引，则可以用来进行搜索。默认值就是true
- false：字段不会被索引，不能用来搜索
index的默认值就是true，也就是说你不进行任何配置，所有字段都会被索引。

但是有些字段是我们不希望被索引的，比如企业的logo图片地址，就需要手动设置index为false。

### store
是否将数据进行独立存储。

原始的文本会存储在`_source`里面，默认情况下其他提取出来的字段都不是独立存储的，是从`_source`里面提取出来的。当然你也可以独立的存储某个字段，只要设置store:true即可，获取独立存储的字段要比从_source中解析快得多，但是也会占用更多的空间，所以要根据实际业务需求来设置，默认为false。

### analyzer

一般我们处理中文会选择ik分词器: ik_max_word, ik_smart

## 查看映射关系
```
GET /索引名称/_mapping
```

## 修改索引映射
```
PUT /索引库名/_mapping
{
  "properties": {
    "字段名": {
      "type": "类型",
      "index": true，
      "store": true，
      "analyzer": "分词器"
    }
  }
}
```
注意:修改映射增加字段 做其它更改只能删除索引 重新建立映射

## 一次性创建索引和映射
```
put /索引库名称
{
  "settings":{
    "索引库属性名":"索引库属性值"
  },
  "mappings":{
    "properties":{
      "字段名":{
        "映射属性名":"映射属性值"
      }
    }
  }
}
```