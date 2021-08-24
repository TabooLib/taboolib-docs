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

API
=====

**糟糕的做法**

.. code-block:: kotlin

    interface API {

        fun doSomething(function: (String) -> Unit)
    }

**推荐的做法**

.. code-block:: kotlin

    import java.util.function.*

    interface API {

        fun doSomething(function: Consumer<String>)
    }

因 TabooLib 会在编译插件时对 Kotlin 引用进行重定向，所以在编写对外开放的 API 时不允许使用 Kotlin 接口。内部使用则没有此条限制。

包名及混淆
==========

**糟糕的做法**

.. code-block:: kotlin

    package com.github.username.taboolib

因 TabooLib 中的部分行为基于绝对路径，所以在项目的包名中不允许出现 ``kotlin`` 或 ``taboolib`` 关键字，在混淆时也必须排除 ``taboolib`` 包下的所有内容。