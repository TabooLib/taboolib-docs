=========
Minecraft-Version 获取游戏版本
=========

对于Minecraft-Version，TabooLib 定义了一套规则，将游戏版本返回Int类型，对NMS跨版本操作具有重要作用

.. note::

    文档不实时更新，可以查看 `源代码 <https://github.com/TabooLib/TabooLib/blob/master/module-nms/src/main/kotlin/taboolib/module/nms/MinecraftVersion.kt>`_
    翻阅本文主要对难以访问 GitHub 的开发者更友好

MinecraftVersion.major
=====

.. csv-table::
   :header: "实际版本", "对应Int"
   :widths: 3, 7
   
   "1.8，1.8.3，1.8.4，1.8.5，1.8.6，1.8.7，1.8.8，1.8.9", "0"
   "1.9，1.9.2，1.9.4", "1"
   "1.10.2", "2"
   "1.11，1.11.2", "3"
   "1.12，1.12.1，1.12.2", "4"
   "1.13，1.13.1，1.13.2", "5"
   "1.14，1.14.1，1.14.2，1.14.3，1.14.4", "6"
   "1.15，1.15.1，1.15.2", "7"
   "1.16.1，1.16.2，1.16.3，1.16.4，1.16.5", "8"
   "1.17，1.17.1", ">=9 / MinecraftVersion.isUniversal(>=9)"



MinecraftVersion.minor
=====

    获取次版本 1.17 是 0， 1.17.1 是 1
