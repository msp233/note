### RESTful API
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
![39ab28e0278ea13aed58ed2446421132.png](evernotecid://2E3F4FCD-9696-48F9-B350-F525479C0FEB/appyinxiangcom/9961630/ENResource/p485)
<img src='https://github.com/msp233/note/blob/master/imgs/RESTful响应内容.jpg' alt="RESTful请求响应结果"/>
[RESTful请求响应结果](https://github.com/msp233/note/blob/master/imgs/RESTful响应内容.jpg)
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
