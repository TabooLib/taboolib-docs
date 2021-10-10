========
参数容器
========

用于解析一种特定规范的字符串工具，具体表现在 ``taboolib.common5.Demand`` 类中。使用方式如下：

.. code-block:: kotlin

    val de = Demand("teleport bukkitObj -x 10 -y 0 -z 20 --force")
    val namespace = de.namespace // teleport
    val player = de.get(0) // 指向没有定义参数名称的第 1 个参数：bukkitObj
    val x = de.get("x") // 10
    val y = de.get("y") // 0
    val z = de.get("z") // 20
    val force = de.tags.contains("force") // true