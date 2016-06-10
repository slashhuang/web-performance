## web性能优化要点

### 网页分析工具及浏览器API
> 分析资源瀑布: 常用工具(webPageTest)
> 浏览器API: navigation timing, User Timing, Performance Timing
    
### 针对浏览器的优化建议
1. 基于文档进行优化【优先获取资源、提前解析等】
    - 优化安排关键网络资源
    - 提前解析
2. 推测性优化
    - DNS预解析
    - TCP预连接
    - 页面预渲染
    
### 一般的做法
- 优化页面结构
- 嵌入提示
    1. 预解析特定域名<link rel='dns-prefetch' href='//slashhuang.github.io'/>
    2. 预取得关键性资源<link rel='subresource' href='/app.js'/>  
    3. 预取得资源<link rel='prefetch' href='/big.jpeg'/>
    4. 预渲染特定页面<link rel='prerender' href='/app.html'/>