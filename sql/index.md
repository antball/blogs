[MySQL索引背后的数据结构及算法原理](http://blog.jobbole.com/24006/)

[mysql生成订单编号函数](https://www.cnblogs.com/working/p/5624666.html)
[ Mysql 存在既更新，不存在就添加（sql语句）](http://blog.csdn.net/woshihaiyong168/article/details/75082668)



### sql三范式

   * 列的原子性，列不能再分
        【联系人】（姓名，性别，电话《家庭电话、工作电话》）
   * 必须有一个主键，其它列要完全依赖主键，不能只依赖主键的一部分
        【OrderDetail】（OrderID，ProductID，UnitPrice，Discount，Quantity，ProductName）
         拆分成：
            【OrderDetail】（OrderID，ProductID，Discount，Quantity）
            【Product】（ProductID，UnitPrice，ProductName）
   * 其它非主键必须直接依赖主键，不能传递依赖主键
        【Order】（OrderID，OrderDate，CustomerID，CustomerName，CustomerAddr，CustomerCity）
            拆分为：
            【Order】（OrderID，OrderDate，CustomerID）和
            【Customer】（CustomerID，CustomerName，CustomerAddr，CustomerCity）

[关于SQL数据库中的范式](http://blog.csdn.net/sinat_35512245/article/details/52923516)

[Redis 和 Memcached 的区别](https://www.cnblogs.com/maweiba/p/6089664.html)