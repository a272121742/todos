分离数据库
=====

##  directions

Schema的封装已经到位，现在需要将其中的Collection从中抽离出来。

0.  将内置在Schema中的数据库变量进行提取
0.  分离两种Collection模型，一种初始化模型，一种动态化模型
0.  初始化模型生成动态化模型
0.  Server端将动态化模型传入Client端，让Client实现模型同步

##  result

可行。

Meteor分为Client和Server，每次程序启动时，Server端和Client的init程序不会执行，只有第一个请求Client的时候，Server最先执行init过程，执行完成后Client得到响应，跟着也执行init。Client的Collection和Server的Collection是两个不同的集合，而我们存在两种Collection。一种是固定的Collection，例如Schema、Validation等，这些资源是作为系统固有资源存在，且利用他们能生成动态Collection。另一种就是动态Collection，动态资源都是由固定的Collection在被初始化后从数据库中读取生成的。但是这会有一个问题，Server端只会init一次，而Client是可以重复init的，例如在客户端刷新之后。而刷新之后动态初始化的类容都将被重置，例如动态的Collection。因此我们要做的就是在Client每次init的时候，重新去Server端口取一次数据，以保证前后端的一致性。
