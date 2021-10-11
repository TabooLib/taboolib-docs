=============
module-nms
=============

这部分提供了一些必要的 Bukkit 平台服务端逆向工具。

**该模块依赖于：**

* common
* platform-bukkit

**安装方式如下所示：**

.. code-block:: kotlin

    taboolib {
        install("common", "module-nms")
        // 依赖平台
        install("platform-bukkit")
    }

内容
========

.. toctree::
    :maxdepth: 2
    :titlesonly:

    version
    transfer
    packet
    reflect