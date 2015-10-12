# JSON 服务器

[作者 README](./README-json-server.md)

在不需要书写代码的情况下，获取一个完整的假数据 REAST API 只需要 30 秒（我是认真的）。

如果同时使用 [Postman](http://getpostman.com/) 一款功能强大的网页调试与模拟发送网页 HTTP 请求的 Chrome 插件，则真真的能实现前后端完全分离。

## 基础环境：

- [Node.js](https://nodejs.org)
- npm
- Chrome 插件 Postman

### 查看环境：

```bash
$ node -v 
v0.10.35
$ npm -v
2.1.18
```

## `JSON-server` 实例

1.创建`db.json`文件
```json
{
  "posts": [
    {
      "id": 1,
      "title": "json-server",
      "author": "typicode"
    },
    {
      "id": 2,
      "title": "json-server",
      "author": "typicode2"
    },
    {
      "id": 3,
      "title": "json-server",
      "author": "typicode3"
    },
    {
      "id": 4,
      "title": "fy-server",
      "author": "typicode3"
    },
    {
      "id": 5,
      "title": "fy-server",
      "author": "typicode3"
    }
  ],
  "comments": [
    {
      "id": 1,
      "body": "some comment",
      "postId": 1
    },
    {
      "id": 2,
      "body": "some comment",
      "postId": 1
    },
    {
      "id": 3,
      "body": "some comment",
      "postId": 2
    }
  ],
  "profile": {
    "name": "typicode"
  }
}
```

2.安装`json-server`

```bash
$ npm install -g json-server
```

3.启动`json-server`

```bash
json-server --watch db.json
```

4.访问数据

[http://localhost:3000/](http://localhost:3000/)

### JSON-server 路由

#### 过滤器(Filter)

使用`.`访问深层数据

```
GET /posts?title=json-server&author=typicode
GET /posts?id=1&id=2
GET /comments?author.name=typicode
```

#### 数据分页(Slice) `_start` `_end` `_limit`

```
GET /posts?_start=20&_end=30
GET /posts/1/comments?_start=20&_end=30
GET /posts/1/comments?_start=20&_limit=10
```

#### 分类(Sort) `_sort` `_order`（DESC ASC）

```
GET /posts?_sort=views&_order=DESC
GET /posts/1/comments?_sort=votes&_order=ASC
```

#### 范围(Range) `_gte` `_lte`

```
GET /posts?views_gte=10&views_lte=20
```

#### 搜索(Full-text search) `q`

```
GET /posts?q=internet
```

#### 关系数据(Relationships) `_embed ` `_expand` `/`

`_embed` 包含子类数据
`_expand` 包含父类数据

```
GET /posts?_embed=comments
GET /posts/1?_embed=comments
```

```
GET /comments?_expand=post
GET /comments/1?_expand=post
```

```
GET /posts/1/comments
```

#### 获取所有假数据

```
GET /db
```


### JSON-server 路由配置


