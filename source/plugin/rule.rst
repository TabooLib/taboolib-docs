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

