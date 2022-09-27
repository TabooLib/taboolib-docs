==========
指令帮助
==========

快速生成你的插件指令帮助。

**该模块依赖于：**

* common

**具体表现为以下扩展函数：**

.. code-block:: kotlin

    fun CommandBuilder.CommandComponent.createHelper()

使用方式
~~~~~~~~

.. code-block:: kotlin

    @CommandBody
    val main = mainCommand {
        createHelper()
    }

.. code-block:: kotlin
    command("command") {
        createHelper()
        literial("sub") {
            // ...
        }
    }
