分离数据库
=====

##  directions

Schema的封装已经到位，现在需要将其中的Collection从中抽离出来。

0.  将内置在Schema中的数据库变量进行提取
0.  分离两种Collection模型，一种初始化模型，一种动态化模型
0.  初始化模型生成动态化模型
0.  Server端将动态化模型传入Client端，让Client实现模型同步

##  result
