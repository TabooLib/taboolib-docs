========
插件实例
========

虽然基于 TabooLib 开发的插件中没有插件实例（Plugin Instance）这一概念，但是由于一些必要的限制，我们需要获取由当前运行平台所定义的插件实例。

.. note::

    例如在 Bukkit 平台下我们注册 Service 或是修改 Metadata 都需要借助插件实例来完成。

各平台获取插件实例方式如下
=======================

.. csv-table::
   :header: "平台", "对应"
   :widths: 1, 2
   
   "bukkit", "``BukkitPlugin.getInstance()``"
   "nukkit", "``NukkitPlugin.getInstance()``"
   "bungee", "``BungeePlugin.getInstance()``"
   "sponge-api7", "``Sponge7Plugin.getInstance()``"
   "sponge-api8", "``Sponge8Plugin.getInstance()``"
   "velocity", "``VelocityPlugin.getInstance()``"

.. warning::

   除非在 ``@PlatformImplementations`` 下，无论何时，我们都不建议频繁获取和使用插件实例。这极大程度的增加了多平台移植工作难度。