=================
module-database
=================

这部分作为数据库工具，基于 HikariCP 连接池。不同于 Exposed 框架，不会将数据映射到对象。

**该模块依赖于：**

* common
* module-configuration（可选）

**安装方式如下所示：**

.. code-block:: kotlin

    taboolib {
        install("common", "module-database")
        // 可选
        install("module-configuration")
    }

内容
========

.. toctree::
    :maxdepth: 2
    :titlesonly:

    host
    table
    workspace
    query