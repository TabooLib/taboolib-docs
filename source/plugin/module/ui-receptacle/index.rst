=====================
module-ui-receptacle
=====================

这部分作为 Bukkit 平台的虚拟容器构建工具，完全由数据包实现。基于原 TrMenu 的代码改进而成。

**该模块依赖于：**

* common
* module-nms
* platform-bukkit

**安装方式如下所示：**

.. code-block:: kotlin

    taboolib {
        install("common", "module-nms", "module-ui-receptacle")
        // 依赖平台
        install("platform-bukkit")
    }

内容
========

.. toctree::
    :maxdepth: 2
    :titlesonly:

    type
    event