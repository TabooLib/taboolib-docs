==========
扩展方法
==========

有关NMS的其它拓展工具,具体表现为以下顶级或扩展函数：**

.. code-block:: kotlin

    /**
     * 生成实体并在生成之前执行特定行为
     */
    fun <T : Entity> Location.spawnEntity(entity: Class<T>, func: Consumer<T>)

    /**
     * 调整图片分辨率
     * 地图最佳显示分辨率为128*128
     *
     * @parma width 宽度
     * @parma height 高度
     * @return 缓冲区图像
     */
    fun BufferedImage.zoomed(width: Int = 128, height: Int = 128): BufferedImage
