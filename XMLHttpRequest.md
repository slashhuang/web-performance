## XMLHttpRequest
> 这个实在是耳熟能详，记录下容易被忽略的东西

### 跨域处理(CORS)
1. 简单版本的处理: 服务端响应首部包含 Access-Control-Allow-Origin:  yourURL.即可
2. 启用cookie和认证等用户凭据: 添加withCredentials。这里的请求流程还会多一个preFlight

### 上传及下载
1. blob(二进制大对象接口，只能查询大小、类型及切割，提供了JS中API的高效互操机制)
    - 支持slice操作
    - 在slice的同时，需要设置`Content-Range`来设置上传数据的uploadSize/blob.size

### 对流的处理
- 上传时候，send只支持完整的载荷
- response，responseText，responseXML也不是为流而设计的。

> 当然通过readyState来监测部分返回，还是可以模拟下流式下载，不过也仅仅局限在文本数据中

### 最后的一个场景
1. 轮询
    - 定时轮询
    - 长轮询