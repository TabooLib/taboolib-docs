==========
告示牌捕获
==========

关于告示牌捕获的工具，具体表现为以下扩展函数：

.. code-block:: kotlin

    /**
     * 捕获玩家在告示牌中输入的内容
     *
     * @param lines 告示牌内容
     * @param function 方法
     */
    fun Player.inputSign(lines: Array<String> = arrayOf(), function: (lines: Array<String>) -> Unit)