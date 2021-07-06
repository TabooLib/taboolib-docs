========
构建系统
========

在前面的准备工作中我们已经安装了 Gradle 构建工具，它可以帮助你管理你的项目的构建过程。作为一个和 IDE 无关的工具，你可以使用它来管理你对 TabooLib 或者其他的插件的依赖，同时给予其他人一种方便的方式通过源代码构建你的插件。

.. warning::

    对于基于 TabooLib 的插件来说是必须使用 Gradle 的，因为它们需要使用 Gradle 插件来进行模块安装和源代码处理。

Gradle 使用基于 `Groovy <https://www.groovy-lang.org/>`_ 或 `Kotlin <https://kotlinlang.org/>`_ 的脚本来配置项目。一个 Gradle 项目通常包含在你的项目的根目录中，并通过 ``build.gradle`` 这一文件告诉 Gradle 如何构建这一项目。

.. tip::

    请参阅 :doc:`/preparing/gradle` 以了解 Gradle 是如何安装的和一些相关的一般概念。

首先按照 :doc:`env/index` 设置你的开发环境，然后按照 :doc:`project/index` 说的去做。
