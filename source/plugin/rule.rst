===========
插件开发约定
===========

这一部分将介绍一些开发准则和惯例，有的应当遵守，而有的有的应当避免。

初始化属性
==========

**推荐的做法**

.. code-block:: kotlin

    val myFile by lazy { newFile(getDataFolder(), "myfile.txt") }

**糟糕的做法**

.. code-block:: kotlin

    val myFile = newFile(getDataFolder(), "myfile.txt")

在初始化属性时引用基于平台（Platform Side）的方法时，可能会触发 NPE 并产生该类的初始化错误。这种情况下我们推荐使用 Kotlin 所提供的 ``by lazy`` 关键字。

混淆
=====

因 TabooLib 中的部分行为基于绝对路径，所以在混淆时必须排除 ``taboolib`` 包下的所有内容。下面是一段代码节选。

.. code-block:: kotlin

    override fun getOpenContainers(): List<OpenContainer> {
        return Bukkit.getPluginManager().plugins.filter { it.javaClass.name.endsWith("platform.BukkitPlugin") }.mapNotNull {
            pluginContainer.computeIfAbsent(it.name) { _ -> BukkitOpenContainer(it) }
        }
    }
