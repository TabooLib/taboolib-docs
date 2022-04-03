========
创建连接
========

在基本使用方法中并**没有**实际创建一个**表**的存在，只是声明了一个表的**格式**。
在稍后的**创建表**中会告知如何创建一个具体存在的表

基本使用方法
========

.. code-block:: kotlin
    
    private val host = confDatabase.getHost("MySQL")
    private val tableVar = Table("表名", host) {
        add { id() }
        // 这里声明了一个uid列，并且作为了主键。
        add("uid") {
            // 指定了这个列的数据类型
            type(ColumnTypeSQL.VARCHAR, 64) {
                // 设置这个列为KEY
                options(ColumnOptionSQL.KEY)
            }
        }
        // 这里声明了一个data列
        add("data") {
            // 指定这个列的数据类型
            type(ColumnTypeSQL.TEXT)
        }
    }

    override fun host(): Host<*> {
        return host
    }

    override fun tableVar(): Table<*, *> {
        return tableVar
    }
    
在**配置文件**中应该有一个这样的**键值对**用来告诉程序数据的**地址、端口**等信息
    
.. code-block:: yml

  MySQL:
    # 地址
    host: "localhost"
    # 端口
    # 默认值：3306
    port: 3306
    # 用户名
    # 默认值：root
    username: "root"
    # 密码
    # 默认值：root
    password: "root"
    # 数据库名称
    # 指存放到哪一个数据库中
    database: "minecraft"
    # 表前缀
    # 指表名的前缀
    TablePrefix: "minecraft"
