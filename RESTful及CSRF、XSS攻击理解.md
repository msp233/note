### 一、RESTful API
简单的说：RESTful是一种架构的规范与约束、原则，符合这种规范的架构就是RESTful架构。
 
先看REST是什么意思，英文Representational state transfer 表述性状态转移 其实就是对 资源 的表述性状态转移。
资源的地址 在web中就是URL （统一资源标识符）
资源是REST系统的核心概念。 所有的设计都是以资源为中心.

RESTful 架构的核心规范与约束：统一接口
分为四个子约束：
1.每个资源都拥有一个资源标识，每个资源的资源标识可以用来唯一地标明该资源
2.消息的自描述性
3.资源的自描述性。
4.HATEOAS Hypermedia As The Engine Of Application State(超媒体作为应用状态引擎)
即客户只可以通过服务端所返回各结果中所包含的信息来得到下一步操作所需要的信息，如到底是向哪个URL发送请求等。也就是说，一个典型的REST服务不需要额外的文档标示通过哪些URL访问特定类型的资源，而是通过服务端返回的响应来标示到底能在该资源上执行什么样的操作
<img src='https://github.com/msp233/note/blob/master/imgs/RESTful响应内容.jpg' alt="RESTful请求响应结果"/>
在设计web接口的时候，REST主要是用于定义接口名，接口名一般是用名次写，不用动词，通过请求类型进行区分。
例如：
1. get 表查找
2. post 表添加
3. put 表更新
4. delete 表删除

#### GET 
- 安全且幂等
- 获取表示
- 变更时获取表示（缓存）
- 200（OK） - 表示已在响应中发出
- 204（无内容） - 资源有空表示
- 301（Moved Permanently） - 资源的URI已被更新
- 303（See Other） - 其他（如，负载均衡）
- 304（not modified）- 资源未更改（缓存）
- 400 （bad request）- 指代坏请求（如，参数错误）
- 404 （not found）- 资源不存在
- 406 （not acceptable）- 服务端不支持所需表示
- 500 （internal server error）- 通用错误响应
- 503 （Service Unavailable）- 服务端当前无法处理请求
#### POST

* 不安全且不幂等
* 使用服务端管理的（自动产生）的实例号创建资源
* 创建子资源
* 部分更新资源
* 如果没有被修改，则不过更新资源（乐观锁）
* 200（OK）- 如果现有资源已被更改
* 201（created）- 如果新资源被创建
* 202（accepted）- 已接受处理请求但尚未完成（异步处理）
* 301（Moved Permanently）- 资源的URI被更新
* 303（See Other）- 其他（如，负载均衡）
* 400（bad request）- 指代坏请求
* 404 （not found）- 资源不存在
* 406 （not acceptable）- 服务端不支持所需表示
* 409 （conflict）- 通用冲突
* 412 （Precondition Failed）- 前置条件失败（如执行条件更新时的冲突）
* 415 （unsupported media type）- 接受到的表示不受支持
* 500 （internal server error）- 通用错误响应
* 503 （Service Unavailable）- 服务当前无法处理请求

#### PUT

* 不安全但幂等
* 用客户端管理的实例号创建一个资源
* 通过替换的方式更新资源
* 如果未被修改，则更新资源（乐观锁）
* 200 （OK）- 如果已存在资源被更改
* 201 （created）- 如果新资源被创建
* 301（Moved Permanently）- 资源的URI已更改
* 303 （See Other）- 其他（如，负载均衡）
* 400 （bad request）- 指代坏请求
* 404 （not found）- 资源不存在
* 406 （not acceptable）- 服务端不支持所需表示
* 409 （conflict）- 通用冲突
* 412 （Precondition Failed）- 前置条件失败（如执行条件更新时的冲突）
* 415 （unsupported media type）- 接受到的表示不受支持
* 500 （internal server error）- 通用错误响应
* 503 （Service Unavailable）- 服务当前无法处理请求

#### DELETE 

* 不安全但幂等
* 删除资源
* 200 （OK）- 资源已被删除
* 301 （Moved Permanently）- 资源的URI已更改
* 303 （See Other）- 其他，如负载均衡
* 400 （bad request）- 指代坏请求
* 404 （not found）- 资源不存在
* 409 （conflict）- 通用冲突
* 500 （internal server error）- 通用错误响应
* 503 （Service Unavailable）- 服务端当前无法处理请求


### 二、CSRF
CSRF（Cross-site request forgery）跨站请求伪造，也被称为“One Click Attack”或者Session Riding，通常缩写为CSRF或者XSRF，是一种对网站的恶意利用。尽管听起来像跨站脚本（XSS），但它与XSS非常不同，**XSS利用站点内的信任用户**，而**CSRF则通过伪装来自受信任用户的请求来利用受信任的网站**。与XSS攻击相比，CSRF攻击往往不大流行（因此对其进行防范的资源也相当稀少）和难以防范，所以被认为比XSS更具危险性。

一般通过获取用户的session、cookie信息，进行伪造正常用户的各种操作。

##### 图示：
<img src="https://github.com/msp233/note/blob/master/imgs/CSRF攻击.jpg" alt="CSRF攻击.jpg"/>

##### 举例： 
CSRF攻击的主要目的是让用户在不知情的情况下攻击自己已登录的一个系统，类似于钓鱼。如用户当前已经登录了邮箱，或bbs，同时用户又在使用另外一个，已经被你控制的站点，我们姑且叫它钓鱼网站。这个网站上面可能因为某个图片吸引你，你去点击一下，此时可能就会触发一个js的点击事件，构造一个bbs发帖的请求，去往你的bbs发帖，由于当前你的浏览器状态已经是登陆状态，所以session登陆cookie信息都会跟正常的请求一样，纯天然的利用当前的登陆状态，让用户在不知情的情况下，帮你发帖或干其他事情。

##### CSRF防御
通过 referer、token 或者 验证码 来检测用户提交。
尽量不要在页面的链接中暴露用户隐私信息。
对于用户修改删除等操作最好都使用post 操作 。
避免全站通用的cookie，严格设置cookie的域。

### 三、XSS攻击
跨站脚本攻击(Cross Site Scripting)，为了不和层叠样式表(Cascading Style Sheets, CSS)的缩写混淆，故将跨站脚本攻击缩写为XSS。恶意攻击者往Web页面里插入恶意Script代码，当用户浏览该页之时，嵌入其中Web里面的Script代码会被执行，从而达到恶意攻击用户的目的。

##### XSS攻击分成两类
- 一类是来自内部的攻击，主要指的是利用程序自身的漏洞，构造跨站语句，如:dvbbs的showerror.asp存在的跨站漏洞。
- 另一类则是来自外部的攻击，主要指的自己构造XSS跨站漏洞网页或者寻找非目标机以外的有跨站漏洞的网页。如当我们要渗透一个站点，我们自己构造一个有跨站漏洞的网页，然后构造跨站语句，通过结合其它技术，如社会工程学等，欺骗目标服务器的管理员打开。

##### XSS划分：
**存储型和反射型**
1. **存储型XSS：**
存储型XSS，持久化，代码是存储在服务器中的，如在个人信息或发表文章等地方，加入代码，如果没有过滤或过滤不严，那么这些代码将储存到服务器中，用户访问该页面的时候触发代码执行。这种XSS比较危险，容易造成蠕虫，盗窃cookie（虽然还有种DOM型XSS，但是也还是包括在存储型XSS内）。
2. **反射型XSS：**
非持久化，需要欺骗用户自己去点击链接才能触发XSS代码（服务器中没有这样的页面和内容），一般容易出现在**搜索页面**。

#### 究其原因：
**主要原因：** 过于信任客户端提交的数据！

**解决办法：** 不信任任何客户端提交的数据，只要是客户端提交的数据就应该先进行相应的过滤处理然后方可进行下一步的操作。

**进一步分析细节：**
　　客户端提交的数据本来就是应用所需要的，但是恶意攻击者利用网站对客户端提交数据的信任，在数据中插入一些符号以及javascript代码，那么这些数据将会成为应用代码中的一部分了。那么攻击者就可以肆无忌惮地展开攻击啦。

　　因此我们绝不可以信任任何客户端提交的数据！！！


#### 防范措施：
XSS漏洞是Web应用程序中最常见的漏洞之一。如果您的站点没有预防XSS漏洞的固定方法，那么就存在XSS漏洞。这个利用XSS漏洞的病毒之所以具有重要意义是因为，通常难以看到XSS漏洞的威胁，而该病毒则将其发挥得淋漓尽致。
- 过滤HTML实体

    1. 将重要的cookie标记为http only, 这样的话Javascript 中的document.cookie语句就不能获取到cookie了.

    2. 表单数据规定值的类型，例如：年龄应为只能为int、name只能为字母数字组合。。。。

    3. 对数据进行Html Encode 处理

    4. 过滤或移除特殊的Html标签， 例如: <script>, <iframe> , &lt; for <, &gt; for >, &quot for

    5. 过滤JavaScript 事件的标签。例如 "onclick=", "onfocus" 等等。

- 特别注意：
    在有些应用中是允许html标签出现的，甚至是javascript代码出现。因此我们在过滤数据的时候需要仔细分析哪些数据是有特殊要求（例如输出需要html代码、javascript代码拼接、或者此表单直接允许使用等等），然后区别处理！
- PHP中的相应函数
```php
strip_tags($str, [允许标签])  #从字符串中去除 HTML 和 PHP 标记

htmlentities($str)函数    #转义html实体

html_entity_decode($str)函数    #反转义html实体

addcslashes($str, ‘字符’)函数     #给某些字符加上反斜杠

stripcslashes($str)函数          #去掉反斜杠

addslashes ($str )函数          #单引号、双引号、反斜线与 NULL加反斜杠

stripslashes($str)函数           #去掉反斜杠

htmlspecialchars()              #特殊字符转换为HTML实体

htmlspecialchars_decode()       #将特殊的 HTML 实体转换回普通字符
```
