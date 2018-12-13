### 一、RESTful API
简单的说：RESTful是一种架构的规范与约束、原则，符合这种规范的架构就是RESTful架构。
 
先看REST是什么意思，英文Representational state transfer 表述性状态转移 其实就是对 资源 的表述性状态转移。
资源的地址 在web中就是URL （统一资源标识符）
资源是REST系统的核心概念。 所有的设计都是以资源为中心

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

