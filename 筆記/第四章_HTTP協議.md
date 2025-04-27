# HTTP 简介



<img src="images/1681522600239.png" alt="1681522600239" style="zoom:67%;" />



> **HTTP 超文本传输协议** (HTTP-Hyper Text transfer protocol)，是一个属于应用层的面向对象的协议，由于其简捷、快速的方式，适用于分布式超媒体信息系统。它于1990年提出，经过十几年的使用与发展，得到不断地完善和扩展。**它是一种详细规定了浏览器和万维网服务器之间互相通信的规则**，通过因特网传送万维网文档的数据传送协议。客户端与服务端通信时传输的内容我们称之为**报文**。**HTTP协议就是规定报文的格式。**HTTP就是一个通信规则，这个规则规定了客户端发送给服务器的报文格式，也规定了服务器发送给客户端的报文格式。实际我们要学习的就是这两种报文**。客户端发送给服务器的称为"请求报文**"，**服务器发送给客户端的称为"响应报文"**。

## 发展历程

### HTTP/0.9 

+ 蒂姆伯纳斯李是一位英国计算机科学家，也是万维网的发明者。他在 1989 年创建了单行 HTTP 协议。它只是返回一个网页。这个协议在 1991 年被命名为 HTTP/0.9。 

### HTTP/1.0

+  1996 年，HTTP/1.0 发布。该规范是显著扩大，并且支持三种请求方法：GET、Head 和 POST。 
+  HTTP/1.0 相对于 HTTP/0.9 的改进如下：
   + 每个请求都附加了 HTTP 版本。
   + 在响应开始时发送状态代码。
   + 请求和响应都包含 HTTP 报文头。
   + 内容类型能够传输 HTML 文件以外的文档。
+  但是，HTTP/1.0 不是官方标准。

### HTTP/1.1

+ HTTP 的第一个标准化版本 HTTP/1.1 ( RFC 2068 ) 于 1997 年初发布，支持七种请求方法：OPTIONS、GET、HEAD、POST、PUT、DELETE，和 TRACE 

+ HTTP/1.1 是 HTTP 1.0 的增强：

  + 虚拟主机允许从单个 IP 地址提供多个域。

  + 持久连接和流水线连接允许 Web 浏览器通过单个持久连接发送多个请求。

  + 缓存支持节省了带宽并使响应速度更快。

+ HTTP/1.1 在接下来的 15 年左右将非常稳定。 

+ 在此期间，出现了 HTTPS（安全超文本传输协议）。它是使用 SSL/TLS 进行安全加密通信的 HTTP 的安全版本。 

### HTTP/2

+  由 IETF 在 2015 年发布。HTTP/2 旨在提高 Web 性能，减少延迟，增加安全性，使 Web 应用更加快速、高效和可靠。 

- 多路复用：HTTP/2 允许同时发送多个请求和响应，而不是像 HTTP/1.1 一样只能一个一个地处理。这样可以减少延迟，提高效率，提高网络吞吐量。
- 二进制传输：HTTP/2 使用二进制协议，与 HTTP/1.1 使用的文本协议不同。二进制协议可以更快地解析，更有效地传输数据，减少了传输过程中的开销和延迟。
- 头部压缩：HTTP/2 使用 HPACK 算法对 HTTP 头部进行压缩，减少了头部传输的数据量，从而减少了网络延迟。
- 服务器推送：HTTP/2 支持服务器推送，允许服务器在客户端请求之前推送资源，以提高性能。
- 改进的安全性：HTTP/2 默认使用 TLS（Transport Layer Security）加密传输数据，提高了安全性。
- 兼容 HTTP/1.1：HTTP/2 可以与 HTTP/1.1 共存，服务器可以同时支持 HTTP/1.1 和 HTTP/2。如果客户端不支持 HTTP/2，服务器可以回退到 HTTP/1.1。

### HTTP/3

+ 于 2021 年 5 月 27 日发布，HTTP/3 是一种新的、快速、可靠且安全的协议，适用于所有形式的设备。 HTTP/3 没有使用 TCP，而是使用谷歌在 2012 年开发的新协议 QUIC 
+ HTTP/3 是继 HTTP/1.1 和 HTTP/2 之后的第三次重大修订。 

+ HTTP/3 带来了革命性的变化，以提高 Web 性能和安全性。设置 HTTP/3 网站需要服务器和浏览器支持。

+ 目前，谷歌云、Cloudflare 和 Fastly 支持 HTTP/3。Chrome、Firefox、Edge、Opera 和一些移动浏览器支持 HTTP/3。

## HTTP 协议的会话方式

> 浏览器与服务器之间的通信过程要经历四个步骤

![](images/1557672342250_1H8nt17MNz.png)

-   浏览器与 WEB 服务器的连接过程是短暂的，每次连接只处理一个请求和响应。对每一个页面的访问，浏览器与 WEB 服务器都要建立一次单独的连接。
-   浏览器到 WEB 服务器之间的所有通讯都是完全独立分开的请求和响应对。

## HTTP1.0 和 HTTP1.1 的区别

> 在 HTTP1.0 版本中，浏览器请求一个带有图片的网页，会由于下载图片而与服务器之间开启一个新的连接；但在 HTTP1.1 版本中，允许浏览器在拿到当前请求对应的全部资源后再断开连接，提高了效率。

![](images/1557672415271_EgyN-GdbWY.png)



## 在浏览器中通过 F12 工具抓取请求响应报文包

> 几乎所有的 PC 端浏览器都支持了 F12 开发者工具，只不过不同的浏览器工具显示的窗口有差异

<img src="images/1681522138051.png" alt="1681522138051" style="zoom:80%;" />

# 请求和响应报文

## 报文的格式

> 主体上分为报文首部和报文主体，中间空行隔开

<img src="images/1681522962846.png" alt="1681522962846" style="zoom: 62%;" />



> 报文部首可以继续细分为  "行" 和 "头"

![1681522998417](images/1681522998417.png)

## 请求报文

> 客户端发给服务端的报文

+ 請求報文格式

  + 請求行
    - 請求的方式 
    - 請求的資源路徑[+?+請求參數]
    - 請求的協議版本號

  + 請求頭 : 告知服務與該請求有關的額外資訊。
    - key : value 組成不同的鍵值對，表示不同的含意。
  + 空行 : 位于请求头和请求体之间。这个空行是必需的，它告诉服务器请求头的结束位置，因此服务器知道接下来的内容是请求体而不是请求头的一部分。
  + 請求體 : 就是發送給服務器的數據，POST 请求才有请求体。

> 浏览器  F12 网络下查看请求数据包

![1681524200024](images/1681524200024.png)

### form 表单发送 GET 请求特点

1、由于请求参数在请求首行中已经携带了，所以没有请求体，也没有请求空行
2、请求参数拼接在 url 地址中，地址栏可见 `url?name1=value1&name2=value2` ，不安全
3、由于参数在地址栏中携带，所以有大小限制，**地址栏数据大小一般限制为4k**，只能携带纯文本
4、get 请求参数只能上传文本数据
5、没有请求体。所以封装和解析都快，效率高， 浏览器默认提交的请求都是 get 请求比如：地址栏输入回车、超链接、表单默认的提交方式

#### 查看 GET 请求行、请求头、请求体

+ 请求行组成部分

  + ```http
    GET /05_web_tomcat/login_success.html?username=admin&password=123213 HTTP/1.1
    ```

  + 请求方式  →  GET

  + 访问服务器的资源路径?参数1=值1&参数2=值2 ...  →  `/05_web_tomcat/login_success.html?username=admin&password=123213`

  + 协议及版本  →  HTTP/1.1

+ 请求头

  + ```http
    -主机虚拟地址
    Host: localhost:8080   
    -长连接
    Connection: keep-alive 
    -请求协议的自动升级[http的请求，服务器却是https的，浏览器自动会将请求协议升级为https的]
    Upgrade-Insecure-Requests: 1  
    - 用户系统信息
    User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.75 Safari/537.36
    - 浏览器支持的文件类型
    Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
    - 当前页面的上一个页面的路径[当前页面通过哪个页面跳转过来的]：   可以通过此路径跳转回上一个页面， 广告计费，防止盗链
    Referer: http://localhost:8080/05_web_tomcat/login.html
    - 浏览器支持的压缩格式
    Accept-Encoding: gzip, deflate, br
    - 浏览器支持的语言
    Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
    ```

+ 请求空行

+ 请求体
  + GET 请求数据不放在请求体

### form 表单发送 post 请求特点

1、POST 请求有请求体，而 GET 请求没有请求体。
2、POST 请求数据在请求体中携带，请求体数据大小没有限制，可以用来上传所有内容，例如 :**文件、文本**
3、只能使用 POST 请求上传文件
4、POST 请求报文多了和请求体相关的配置  →  请求头
5、地址栏参数不可见，相对安全
6、POST 效率比 GET 低

+ POST 请求要求将 form 标签的 method 的属性设置为 post

![1681525012046](images/1681525012046.png)

#### 查看 POST 的请求行、请求头、请求体

+ 请求行组成部分

  + ```http
    POST /05_web_tomcat/login_success.html HTTP/1.1
    ```

  + 请求方式  →  POST

  + 访问服务器的资源路径?参数1=值1&参数2=值2 ...  →  `/05_web_tomcat/login_success.html`

  + 协议及版本  →  HTTP/1.1

+ 请求头

  + ```http
    Host: localhost:8080
    Connection: keep-alive
    -请求体内容的长度
    Content-Length: 31     
    -无缓存
    Cache-Control: max-age=0  
    Origin: http://localhost:8080
    -协议的自动升级
    Upgrade-Insecure-Requests: 1  
    -请求体内容类型[服务器根据类型解析请求体参数]
    Content-Type: application/x-www-form-urlencoded   
    User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.75 Safari/537.36
    Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
    Referer: http://localhost:8080/05_web_tomcat/login.html
    Accept-Encoding: gzip, deflate, br
    Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
    Cookie:JSESSIONID-
    ```

+ 请求空行

+ 请求体 : 浏览器提交给服务器的数据

  + ```http
    username=admin&password=1232131
    ```

## 响应报文

- 響應行
  - 響應的協議和版本號
  - 響應狀態碼
  - 響應狀態描述符
- 響應頭 : 告知客戶端與該回應有關的資訊，最後並以空白行代表結束。
  - key : value 組成不同的鍵值對，表示不同的含意。
- 空行
- 響應體 : 傳送客戶端所請求的內容

![1681525347456](images/1681525347456.png)



![1681525384347](images/1681525384347.png)

+ 响应行组成部分

  + ```java
    // 说明：响应协议为HTTP1.1，响应状态码为200，表示请求成功； 
    HTTP/1.1 200 OK
    ```

  + 协议及版本  →  HTTP/1.1

  + 响应状态码  →  200

  + 状态描述  →  OK  (缺省)

+ 响应头

  + ```java
    Server: Apache-Coyote/1.1   //服务器的版本信息
    Accept-Ranges: bytes
    ETag: W/"157-1534126125811"
    Last-Modified: Mon, 13 Aug 2018 02:08:45 GMT
    Content-Type: text/html    //响应体数据的类型[浏览器根据类型解析响应体数据]
    Content-Length: 157   //响应体内容的字节数
    Date: Mon, 13 Aug 2018 02:47:57 GMT  //响应的时间，这可能会有8小时的时区差
    ```

+ 响应体

  + ```html
    <!--需要浏览器解析使用的内容[如果响应的是html页面，最终响应体内容会被浏览器显示到页面中]-->
    
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="UTF-8">
        <title>Insert title here</title>
      </head>
      <body>
        恭喜你，登录成功了...
      </body>
    </html>
    ```

### 响应状态码

> 响应状态码 : 响应码对浏览器来说很重要，它告诉浏览器响应的结果。比较有代表性的响应码如下：

+ **200：** 请求成功，浏览器会把响应体内容（通常是html）显示在浏览器中。
+ **302：** 重定向，当响应码为 302 时，表示服务器要求浏览器重新再发一个请求，服务器会发送一个响应头Location 指定新请求的 URL 地址。
+ **304：** 使用了本地缓存
+ **404：** 请求的资源没有找到，说明客户端错误的请求了不存在的资源。
+ **405：** 请求的方式不允许
+ **500：** 请求资源找到了，但服务器内部出现了错误。

**更多的响应状态码**

| 状态码 | 状态码英文描述                  | 中文含义                                                     |
| :----- | :------------------------------ | :----------------------------------------------------------- |
| 1**    |                                 |                                                              |
| 100    | Continue                        | 继续。客户端应继续其请求                                     |
| 101    | Switching Protocols             | 切换协议。服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如，切换到HTTP的新版本协议 |
| 2**    |                                 |                                                              |
| 200    | OK                              | 请求成功。一般用于GET与POST请求                              |
| 201    | Created                         | 已创建。成功请求并创建了新的资源                             |
| 202    | Accepted                        | 已接受。已经接受请求，但未处理完成                           |
| 203    | Non-Authoritative Information   | 非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本 |
| 204    | No Content                      | 无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档 |
| 205    | Reset Content                   | 重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。可通过此返回码清除浏览器的表单域 |
| 206    | Partial Content                 | 部分内容。服务器成功处理了部分GET请求                        |
| 3**    |                                 |                                                              |
| 300    | Multiple Choices                | 多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择 |
| 301    | Moved Permanently               | 永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替 |
| 302    | Found                           | 临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI |
| 303    | See Other                       | 查看其它地址。与301类似。使用GET和POST请求查看               |
| 304    | Not Modified                    | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源 |
| 305    | Use Proxy                       | 使用代理。所请求的资源必须通过代理访问                       |
| 306    | Unused                          | 已经被废弃的HTTP状态码                                       |
| 307    | Temporary Redirect              | 临时重定向。与302类似。使用GET请求重定向                     |
| 4**    |                                 |                                                              |
| 400    | Bad Request                     | 客户端请求的语法错误，服务器无法理解                         |
| 401    | Unauthorized                    | 请求要求用户的身份认证                                       |
| 402    | Payment Required                | 保留，将来使用                                               |
| 403    | Forbidden                       | 服务器理解请求客户端的请求，但是拒绝执行此请求               |
| 404    | Not Found                       | 服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面 |
| 405    | Method Not Allowed              | 客户端请求中的方法被禁止                                     |
| 406    | Not Acceptable                  | 服务器无法根据客户端请求的内容特性完成请求                   |
| 407    | Proxy Authentication Required   | 请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权 |
| 408    | Request Time-out                | 服务器等待客户端发送的请求时间过长，超时                     |
| 409    | Conflict                        | 服务器完成客户端的 PUT 请求时可能返回此代码，服务器处理请求时发生了冲突 |
| 410    | Gone                            | 客户端请求的资源已经不存在。410不同于404，如果资源以前有现在被永久删除了可使用410代码，网站设计人员可通过301代码指定资源的新位置 |
| 411    | Length Required                 | 服务器无法处理客户端发送的不带Content-Length的请求信息       |
| 412    | Precondition Failed             | 客户端请求信息的先决条件错误                                 |
| 413    | Request Entity Too Large        | 由于请求的实体过大，服务器无法处理，因此拒绝请求。为防止客户端的连续请求，服务器可能会关闭连接。如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息 |
| 414    | Request-URI Too Large           | 请求的URI过长（URI通常为网址），服务器无法处理               |
| 415    | Unsupported Media Type          | 服务器无法处理请求附带的媒体格式                             |
| 416    | Requested range not satisfiable | 客户端请求的范围无效                                         |
| 417    | Expectation Failed              | 服务器无法满足Expect的请求头信息                             |
| 5**    |                                 |                                                              |
| 500    | Internal Server Error           | 服务器内部错误，无法完成请求                                 |
| 501    | Not Implemented                 | 服务器不支持请求的功能，无法完成请求                         |
| 502    | Bad Gateway                     | 作为网关或者代理工作的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应 |
| 503    | Service Unavailable             | 由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中 |
| 504    | Gateway Time-out                | 充当网关或代理的服务器，未及时从远端服务器获取请求           |
| 505    | HTTP Version not supported      | 服务器不支持请求的HTTP协议的版本，无法完成处理               |

# MIME 類型說明

- MIME 是 HTTP 協議的數據類型
- MIME 類型的格式是 "大類型/小類型"，並與某一種文件的擴展名相對應。

**常見的 MIME 類型 :**

|        文件        |        MIME 類型         |
| :----------------: | :----------------------: |
| 超文本標記語言文本 |        text/html         |
|      普通文本      |        text/plain        |
|      RTF 文本      |     application/rtf      |
|      GIF 圖形      |        image/gif         |
|     JPEG 圖形      |        image/jpeg        |
|    au 聲音文件     |       audio/basic        |
|   MIDI 音樂文件    | audio/midi、audio/x-midi |
| RealAudio 音樂文件 |   audio/x-pn-realaudio   |
|     MPEG 文件      |        video/mpeg        |
|      AVI 文件      |     video/x-msvideo      |
|     GZIP 文件      |    application/x-gzip    |
|      TAR 文件      |    application/x-tar     |

