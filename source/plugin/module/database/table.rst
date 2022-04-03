========
创建表
========

在这一章中，会告诉你如何实际的创建一个**表**用来**存储**和**读取数据**。

基本使用方法
========

.. code-block:: kotlin

    private val type by lazy {
        // 这个类指的是你在创建连接那一章中使用的类
        Database()
    }
    // 创建数据源
    private val dataSource = type.host().createDataSource()
    // 在本类实例化的时候进行表的创建工作
    init {
        type.tableVar().workspace(dataSource) {
            createTable()
        }.run()
    }
