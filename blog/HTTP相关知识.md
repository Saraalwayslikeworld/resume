# 前端需知的HTTP知识点

## 1.http报文
HTTP  (HypertextTransferProtocol/超文本传输协议) 是应用层级（application）的数据传输协议。
在应用程序间传输的数据块就是http报文（message）。
报文由3部分组成，
- 起始行（start line），
- 包含属性的首部（header），
- 可选的包含数据的主体部分（body）

请求报文

    <method><request-URL><version>
    <headers>

    <body>


响应报文

    <version><status><reason-phrase>
    <headers>

    <body>

列举一些头部属性
![](http://p5s9qkvol.bkt.clouddn.com/18-7-21/84081085.jpg)
![](http://p5s9qkvol.bkt.clouddn.com/18-7-21/33853775.jpg)

需要着重了解的是响应报文起始行的**状态码**以及控制**缓存**的头部属性。

## 2.http请求方式
1. GET
2. HEADER
类似GET ，但响应报文只有头部，用于查询。
3. POST
常用于创建服务器数据
4. PUT
常用于修改服务器数据
5. DELETE
6. TRACE
7. OPTIONS

## 3.http状态码

    1xx 没问题，请继续
    2xx 响应成功
        "200":成功；"202":已响应，未处理完成
    3xx 重定向或使用缓存  
        "301":资源永久重定向；"304":使用缓存
    4xx 客户端有问题
        "403":无权限访问；"404":找不到资源
    5xx 服务器有问题
        "500":服务器出现错误；"503":服务器正忙

## 4.缓存控制机制

1.指定缓存过期时间（类似食品保质期，某月某日过期）
    
    Expires: Mon,10 Dec 1990 02:25:22GMT。

 缺点：无法监测文件更新，服务器与客户端时间可能不一致。

2.指定过期的相对时间（类似化妆品的保质期，开盖后6个月）

    cache-control: max-age = 400s 

缺点：无法监测文件更新。

3.过期时间+版本对比
  
增加文件版本编号Etag，当缓存过期后，比对服务器与客户端的文件版本编号，一致则仍使用缓存。
    
    Cache-Control: max-age=300；
    ETag:W/"e-cbxLFQW5zapn79tQwb/g6Q"

缺点： 在分布式系统中，不同服务器相同文件的ETag可能会不同。

4.过期时间+更新时间对比

服务器发给客户端的文件增加Last-Modified声明，表示上次服务器告知的文件修改的时间。当缓存过期，再次向web服务器请求时带上If-Modified-Since，比对服务器文件修改时间和客户端文件修改时间，一致则仍使用缓存。

    Cache-Control: max-age=0
    Last-Modified: Wed, 04 Jul 2018 09:13:54 GMT

    If-Modified-Since: Wed, 04 Jul 2018 09:13:54 GMT


## 5.HTTPS
关于https的原理，有很多文章已经讲得很好啦。简单上幅图。

![](http://p5s9qkvol.bkt.clouddn.com/18-7-21/3669328.jpg)

![](http://p5s9qkvol.bkt.clouddn.com/18-7-21/7562253.jpg)

3.为防止"中间人攻击"，引入第三方“CA证书”，CA为交换信息对象的合法性背书。

**非对称加密 + 对称加密 + CA => HTTPS**