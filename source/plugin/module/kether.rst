===============
module-kether
===============

这部分作为全平台内建脚本（动作语句）解决方案，已经面世许久。在 `这里 <http://kether.tabooproject.org>`__ 查看更多的介绍。

**该模块依赖于：**

* common
* common-5
* module-configuration
* module-chat（可选，提供部分语句）
* module-nms-util（可选，提供部分语句）

**该模块可以与下列模块交互：**

* module-lang（为语言文件提供内联脚本）

**安装方式如下所示：**

.. code-block:: kotlin

    taboolib {
        install("common", "common-5", "module-configuration", "module-kether")
        // 可选
        install("module-chat", "module-nms", "module-nms-util", "module-lang")
    }