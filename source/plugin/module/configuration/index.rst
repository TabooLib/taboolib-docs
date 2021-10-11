======================
module-configuration
======================

这部分作为全平台 Yaml 封装接口与配置文件管理工具，基于大家非常熟悉的 Bukkit Configuration 封装方式。

**该模块依赖于：**

* common
* common-5（可选）
* module-chat（可选）

**安装方式如下所示：**

.. code-block:: kotlin

    taboolib {
        install("common", "module-configuration")
        // 可选
        install("common-5", "module-chat")
    }

内容
========

.. toctree::
    :maxdepth: 2
    :titlesonly:

    config
    localdata
