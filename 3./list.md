# List

传统的列表一般是链表，双向链表、[单向链表](https://gist.github.com/superkevingit/c51b38b3bc27c579aff2d4d6cb7841c2)。
可是python的列表实现方式类似于数组，是一整块单一连续的内存区块。
- 访问操作
    - 遍历：数组和链表的访问速度差不多
    - 指定元素访问：数组更有效率
- 插入操作
    - 链表
        - 操作成本低，无论列表元素数量，时间大致相同
    - 数组
        - 数组移动插入处右边所有元素或整体迁移
        - python的append方法：动态数组或向量
        
        
append(): `theta(1)`

insert(0,): `theta(n)`