# 版本

> 1.0/14.10.10

# 文件路径

`typecho/var/Typecho/Db.php`
`typecho/var/Typecho/Db/Query.php`
`typecho/var/Typecho/Db/Adapter.php`

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

sql(）获取SQL词法构建器实例化对象
实质是实例化一个Typecho_Db_Query对象，在稍后再详细说明

addServer() 为多数据库提供支持

getVersion() 调用适配器方法，返回数据库版本信息

set()设置一个实例化的Typecho_Db对象给内部$_instance变量

get()获取数据库实例化对象,使用静态变量存储实例化对象，可以保证数据库只连接一次

select()使用call_user_func_array()调用sql()返回的Db_Query对象的select()方法，传入筛选参数

update(),delete(),insert()直接调用Db_Query的对应方法

query() 首先判断传入的第一个参数$query是否为Db_Query对象或字符串，如不是直接返回$query,如是Db_Query对象，则操作提取action（查询，插入，更新，删除）信息和op（读写）信息；接着选择连接池并提交查询，最后使用switch根据action不同，返回不同的查询结果resource

fetchAll() 针对查询的操作，参数为查询对象和过滤函数，调用适配器对象的fetch方法，循环放入一个数组，返回所有行

fetchRow() 针对查询操作，仍然是调用fetch方法返回一行

fetchObject() 针对查询操作，调用fectObecjt方法

**超级喜欢使用三目运算符**

```php
//把filter 数组分别赋值给object和method变量
list($object, $method) = $filter;

/*
* 三目运算符
* 判断是否有对应资源，否则返回空数组
* 接着判断是否提供过滤器，否则直接返回行
* 调用过滤器对象的某方法处理后返回
*／
return ($rows = $this->_adapter->fetch($resource)) ?
        ($filter ? $object->$method($rows) : $rows) :
        array();
```

# Db/Query.php

查询操作构造器

# Db/Adpater.php

数据库通用适配接口
