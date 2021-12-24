============
JavaScript
============

将字符串编译为 JavaScript 脚本（基于 Nashorn 引擎）。
**该模块依赖于：**

* common

**使用方式如下：**

.. code-block:: kotlin

    val js = "1 + 1".compileJS()!!
    println(js.eval()) // 2

**传递参数：**

.. code-block:: kotlin

    val js = "1 + value".compileJS()!!
    println(js.eval(SimpleBindings(mapOf("value" to 9)))) // 10