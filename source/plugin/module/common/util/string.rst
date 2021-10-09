==========
字符串相关
==========

关于字符串的部分工具，具体表现为以下顶级函数：

.. code-block:: kotlin

    /**
     * 替换字符串内的变量
     * 例如 "你好, {0}".replaceWithOrder("世界")，速度是 format 的数倍
     */
    fun String.replaceWithOrder(vararg args: Any): String