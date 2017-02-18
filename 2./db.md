# 版本

> 1.0/14.10.10

# 文件路径

`typecho/var/Typecho/Db.php`
`typecho/var/Typecho/Db/Query.php`
`typecho/var/Typecho/Db/Adapter.php`
`typecho/var/Typecho/Db/Exception.php`

# Db.php

首先定义了一系列常量，包括数据库的关键字，如 
   
```sql
const SORT_ASC = 'ASC';
```

接着定义了私有变量：

数据库适配器、默认配置、连接池、已经连接、前缀、适配器名称、实例化的数据库对象

在构造函数中检查数据库适配器是否可用，设置数据库前缀，将连接池和已连接，默认配置都设置为空数组，最后实例化适配器对象

下面几个函数单纯用来返回对象内变量
 * getAdapterName()
 * getPrefix()
 * getConfig()
 
flushPool()将连接池设为空

selectDb()获取相应读或写服务器连接池中的一个 
首先判断是否存在已连接的数据库实例，有则直接返回；没有则会从连接池中随机获取一个

selectDb(）获取SQL词法构建器实例化对象
实质是实例化一个Typecho_Db_Query对象，在稍后再详细说明

addServer() 为多数据库提供支持

getVersion() 调用适配器方法，返回数据库版本信息

set()设置一个实例化的Typecho_Db对象给内部$_instance变量

get()