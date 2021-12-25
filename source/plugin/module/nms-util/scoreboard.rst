==========
记分板
==========

关于计分板的部分工具，具体表现为以下扩展函数：

.. code-block:: kotlin

    /**
     * 发送记分板数据包
     *
     * @param content 记分板内容（设置为空时注销记分板）
     */
    fun Player.sendScoreboard(vararg content: String)
