实时性验证
=====

##  directions

Collection已经大致抽离，如果还没有抽离干净的后面补充实现。现在要解决客户端请求后，服务端会实时性刷新数据。同时服务端更改的数据也要同步到客户端。


##  result

实时性目前还不行，数据库发生变化后需要重新刷新验证规则。
