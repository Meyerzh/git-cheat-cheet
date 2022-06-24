# json server

## Getting started

### Install JSON Server

```bash
$ npm install -g json-server
```

### 创建db.json
Create a `db.json` file with some data
```json
{
  "posts": [
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```

### Start JSON Server

```bash
$ json-server --watch db.json
```

替换端口
```bash
$ json-server --watch db.json --port 3004
```


### 测试接口
你可以使用 postman 测试接口的 post 和 delete 功能。
增加 和 删除

![文档截图](../../assets/Snipaste_2022-06-09_13-09-02.png)