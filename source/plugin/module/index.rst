=====
模块
=====

这部分开始你将真正接触到 TabooLib 的各个模块，在 :doc:`/about/structure` 中了解模块之间的关系。每个模块都需要在构建文件中手动安装才可以使用。

.. code-block:: kotlin

    taboolib {
        // 安装 common 模块
        install("common")
        // 安装 Bukkit 平台实现
        install("platform-bukkit")
    }

若模块之间存在依赖关系，还需要同时安装其对应依赖模块。

.. code-block:: kotlin

    taboolib {
        // 安装 ai 模块
        install("module-ai")
        // 安装 ai 模块所依赖的 nms 模块
        install("module-nms")
    }

.. tips::

    无论在什么情况下，都需要安装 ``common`` 模块以及任意一个平台实现。

内容
========

.. toctree::
    :maxdepth: 4
    :titlesonly:

    common/index
    common-5/index
    ai
    chat
    configuration/index