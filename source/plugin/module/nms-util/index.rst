================
module-nms-util
================

这部分作为 nms 模块的扩展，在基础上增加大量工具。

**该模块依赖于：**

* common
* module-nms
* platform-bukkit

**安装方式如下所示：**

.. code-block:: kotlin

    taboolib {
        install("common", "module-nms", "module-nms-util")
        // 依赖平台
        install("platform-bukkit")
    }

内容
========

.. toctree::
    :maxdepth: 2
    :titlesonly:

    i18n
    light
    nbt
    toast
    map
    scoreboard
    sign
    util