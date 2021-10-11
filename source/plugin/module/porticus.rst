================
module-porticus
================

这部分作为 Bukkit 与 BungeeCord 通讯工具，提供了相当方便的使用方式。

**该模块依赖于：**

* common
* platform-bukkit
* platform-bungeecord

.. tips::

    未来可能会支持 Velocity 平台。

**安装方式如下所示：**

.. code-block:: kotlin

    taboolib {
        install("common", "module-porticus")
        // 依赖平台
        install("platform-bukkit", "platform-bungee")
    }