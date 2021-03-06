## http1.x
### http1.x发展简史
- http0.9: 请求及响应简单，无首部及元数据。
    1. 缺点:缺乏灵活性，仅仅支持超文本类型。
- http1.0: 请求行包含http版本号，随后是请求首部，响应状态紧随其后。
    1. 缺点:对每个请求都打开一个新TCP连接，严重影响性能
- http1.1: 目前主流的网络应用层协议,相比于1.0版本，优化点如下。
    1. 持久连接(默认使用)===> 重用TCP连接
    2. 分块编码传输
    3. 字节范围请求
    4. 增强的缓存机制
    5. 传输编码及请求管道
    
### http 1.x性能要点

#### 《高性能网站建设指南》一书概括的规则
1. 减少DNS查询 （减少请求延迟，避免查询期间阻塞请求）
2. 减少http请求
3. 使用CDN （减少TCP连接网络延迟 + 增加吞吐量）
4. 添加Expires首部及配置ETag标签
5. GZip资源
6. 避免HTTP重定向

#### http1.x特点及性能优化点
1. 持久连接 (减少TCP连接握手成本)
2. http管道将FIFO队列从客户端迁移到服务端(减少一次往返时间，但是会产生`队首阻塞`问题)！！由于实际中不可能出现多路复用,http管道会导致服务器、客户端出现很多微妙的问题。
3. 使用多个TCP连接
    > 由于以上第2点问题的存在，浏览器可以选择在客户端排队所有的http请求，重用持久连接，但这种方式是在太慢。
    于是浏览器开发商选择允许我们打开多个并行TCP会话。   
    - 代价: 多个套接字占用客户端、服务器资源，包括内存、CPU时钟周期
    - TCP流竞争带宽
    - 复杂度提高
    - 应用的并行能力受限
4. 域名分区
    - 缺点: 每个新主机名都要求有一次额外的DNS查询，资源分发域名技术难度还是有点的，运维成本上升。
    - 优点: 多个TCP连接，在资源获取时间上达到了并发的节约。
5. 度量和控制协议开销(合理使用cookie)    
6. 文件的连接与合并
    - 典型的有css sprite
    - 抽离公用的css、js及图片
7. 内联资源
    - 比如webpack
    - base64图片等
