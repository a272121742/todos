关于Meteor不足的解决方案
=====

##  directions

### 限制级API

Meteor.Collection中常用的查询API都有，但是还有一些原生API没有。

> 解决方案：
>
> 0. 除了`find`、`findOne`、`insert`、`update`、`upsesrt`、`remove`这几个API以外，其他的API确实没公布
> 0. 目前查询选项API公开的只有`sort`、`skip`、`limit`、`fields`、`reactive`、`transform`，其他API需证实
> 0. 需要证实，查询是否支持特殊查询参数

### Server端获取Client信息

Meteor能否在Server端获取Client信息。

> 解决方案：
>
> 0. Client端主动发送信息给服务端，并带有客户端信息
> 0. Server端通过NodeJS原生API获取Client相关信息
> 0. 以上解决方案有待证实

### 控制重启

Meteor上传文件后，引起Server重启，连接中的Client也会被迫重启，有无对应的解决方案。

> 解决方案：
>
> 0. Meteor采用的是全app的检测，如果想更改控制，需要修改底层，时间成本和可控性低，不建议使用
> 0. 如果上传的文件或新增文件都是资源文件，可以外联`云资源服务器`，充分利用云服务的特性，降低维护成本
> 0. 在不选用云资源服务器前提下，也可自己搭建资源服务器

### 计算密集

如果计算密集，Meteor消耗时间过大，如何解决

> 解决方案：
>
> 0. Meteor是NodeJS的封装，NodeJS本身不适合计算密集型，应劲量避免
> 0. 如果业务需要，才采用WebServices方式，将计算密集型业务分离出来

### 宕机问题

如果Meteor宕机，如何重启

> 解决方案：
>
> 0. 查找NodeJS相关模块，或者Windows、Linux服务模块，实现智能启动或重启

### 动态模板

Meteor的模板没法动态化，复用率低。

> 解决方案：
>
> 0. 有动态化解决方案，参考DE-Grid技术文档
> 0. 动态化只支持0.8以上版本，0.8以下无法支持

### 浏览器兼容性

Meteor的一些模块在IE下兼容性差

> 解决方案：
>
> 0. Meteor不是一个主前端的框架
> 0. 通过前端方式解决或避开

### 不支持按需加载

客户端请求时，会将所有的模板和前端代码都输送到客户端，导致占用大量的时间。能否按需加载或异步化。

> 解决方案：
>
> 0. 这是Meteor的优势，但项目扩张到边界意外就会形成他的壁垒，目前只能接受他的规范
> 0. 如果动态构造模板可实现，将给解决此问题带来更高的可能

### 弱化的前端

前端没有什么框架，开发起来很混乱。

> 解决方案：
>
> 0. 前端是一个复杂且开放的问题，对于四大框架（结构框架、数据框架、UI框架、响应式框架）难以寻求平衡和兼得
> 0. 招聘资深前端开发工程师，解决前端问题

### 封闭的数据处理

如果不调用`fetch`，没办法对数据进行处理。

> 解决方案：
>
> 0. 通过`transform`方法转换，或者`map`、`forEach`方法
> 0. 或者重新封装数据类型，使之变成可持续迭代的对象

### 模板缺少逻辑

Meteor的模板中有一些常用逻辑缺乏，开发时代码可读性和调试变得复杂。

> 解决方案：
>
> 0. 模板只做数据渲染，不应该做复杂的业务逻辑
> 0. 有用且常用的都已经封装起来，类似于`console`、`switch`、`iteration`等

### 无组件化

Meteor即使解决了模板动态化，依然没有可重用的组件方便开发。

> 解决方案：
>
> 0. 定好基础框架后，就一点点封装组件，这是需要慢慢完善的

### 缺少ORM模型

Meteor所使用的MongoDB数据库没有ORM模型，都需要手工检验。

> 解决方案：
>
> 0. 如果是输出型应用，可以无需ORM模型
> 0. 如果应用带有输入，可以通过引入第三方开发包，通过Schema建立ORM映射

##  result
