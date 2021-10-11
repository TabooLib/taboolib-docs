===========
module-chat
===========

这部分作为全平台 Raw 信息构建工具与 1.16 RGB 颜色转换工具。

**该模块依赖于：**

* common

**安装方式如下所示：**

.. code-block:: kotlin

    taboolib {
        install("common", "module-chat")
    }

Raw 信息构建工具
~~~~~~~~~~~~~~~

该功能具体表现在 ``taboolib.module.chat.Tellrawjson`` 类中，使用方式如下：

.. code-block:: kotlin

    TellrawJson()
        .append("你好")
        .append("世界").hoverText("World!").runCommand("/say HelloWorld!")
        .sendTo(sender)

或是：

.. code-block:: kotlin

    TellrawJson().sendTo(sender) {
        append("你好")
        append("世界").hoverText("World!").runCommand("/say HelloWorld!")
    }

颜色转换
~~~~~~~~

该功能具体表现在以下扩展函数：

.. code-block:: kotlin

    fun String.colored(): String

    fun String.uncolored(): String

    fun List<String>.colored(): List<String>

    fun List<String>.uncolored(): List<String>

同时该方法还支持对高版本中的特殊颜色表达式进行转换，格式如下：

.. code-block:: text

    &{255-255-255} —— RGB 代码
    &{255,255,255} —— RGB 代码
    &{#FFFFFF}     —— HEX 代码