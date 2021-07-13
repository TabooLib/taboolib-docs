=========
插件主类
=========

.. note::
    
    阅读本文档中的所有内容都建立在你已经事先掌握了 Kotlin 知识的基础上。TabooLib 虽然提供了 Minecraft 插件开发基础，但是让你的代码工作和富有创新则取决于你！如果你没有任何 Kotlin 项目的开发经验，那么你可以在 `这里 <https://www.runoob.com/kotlin/kotlin-tutorial.html>`_ 进行初步学习。

新建插件主类
===========

基于 TabooLib 开发的插件中，主类是 **非必需** 的。但是作为一个约定的插件入口，我们应当按照规范创建。这个类可以按照你想要的方式去命名，而且可以使用除了 ``taboolib`` 外的任何一个包。按照惯例，一个类的名称应该首字母大写。

Oracle `推荐 <https://docs.oracle.com/javase/tutorial/java/package/namingpkgs.html>`_ 你去使用你自己的域名作为你的包名。如果你没有域名，那么常见的做法是使用电子邮件（``com.gmail.username.project``），或者一个开源仓库的地址（``io.github.username.project``）。

当你创建好你的主类后，你的主类必须必须继承 ``taboolib.common.platform.Plugin`` 这个类。这样能够让 TabooLib 在读取插件时找到你的主类。下面是演示。

.. code-block:: kotlin

    package io.github.username.project

    import taboolib.common.platform.Plugin

    object ExamplePlugin : Plugin() {

    }

.. note::

    我们建议使用 ``object`` 单例作为插件主类，尽管可以使用 ``class`` 关键字。

插件会在游戏和世界加载前加载。所以对于插件中所有与游戏的交互操作如注册命令或事件，都有着明确的时间界限。而每个运行平台都有自己的生命周期（指游戏阶段的变化）规范，在 TabooLib 中我们对其进行了统一规范。在下面的示例中，当服务器启动时，``onEnable()`` 方法会被调用。

下列示例会在服务器启动时打印一条信息。如果你的插件正确加载了，你会在服务器的初始化输出中找到这条信息。

.. code-block:: kotlin

    package io.github.username.project

    import taboolib.common.platform.*

    object ExamplePlugin : Plugin() {

        override fun onEnable() {
            // 通用日志方法
            info("Successfully running ExamplePlugin!")
        }
    }

有关生命周期的详细解释，请参阅 :doc:`lifecycle` 部分。
