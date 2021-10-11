=============
module-ui
=============

这部分作为 Bukkit 平台的箱子菜单构建工具，提供了数种不同类型的结构。

**该模块依赖于：**

* common
* platform-bukkit

**安装方式如下所示：**

.. code-block:: kotlin

    taboolib {
        install("common", "module-ui")
        // 依赖平台
        install("platform-bukkit")
    }

内容
========

.. toctree::
    :maxdepth: 2
    :titlesonly:

    basic
    linked
    stored