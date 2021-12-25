==========
地图
==========

关于地图的工具，具体表现为以下扩展函数：

.. code-block:: kotlin

    /**
     * MAIN 主手
     * OFF 副手
     */
    enum class Hand {
        MAIN, OFF
    }

    /**
     * 将NMSMap发送给玩家
     *
     * @param player 玩家
     */
     fun NMSMap.sendTo(player: Player)

    /**
     * 构建一个地图
     *
     * @param url 图片地址
     * @param hand 手
     * @param width 宽度
     * @param height 高度
     * @param builder 物品构建器
     * @return NMSMap
     */
    fun buildMap(
        url: String,
        hand: NMSMap.Hand = NMSMap.Hand.MAIN,
        width: Int = 128,
        height: Int = 128,
        builder: ItemBuilder.() -> Unit = {}
    ): NMSMap

    /**
     * 构建一个地图
     *
     * @param file 图片文件
     * @param hand 手
     * @param width 宽度
     * @param height 高度
     * @param builder 物品构建器
     * @return NMSMap
     */
    fun buildMap(
        file: File,
        hand: NMSMap.Hand = NMSMap.Hand.MAIN,
        width: Int = 128,
        height: Int = 128,
        builder: ItemBuilder.() -> Unit = {}
    ): NMSMap

    /**
     * 构建一个地图
     *
     * @param image 缓冲区图像
     * @param hand 手
     * @param width 宽度
     * @param height 高度
     * @param builder 物品构建器
     * @return NMSMap
     */
    fun buildMap(
        image: BufferedImage,
        hand: NMSMap.Hand = NMSMap.Hand.MAIN,
        width: Int = 128,
        height: Int = 128,
        builder: ItemBuilder.() -> Unit = {}
    ): NMSMap

    /**
     * 给玩家构建并发送地图
     *
     * @param url 图片地址
     * @param hand 手
     * @param width 宽度
     * @param height 高度
     * @param builder 物品构建器
     */
    fun Player.sendMap(
        url: String,
        hand: NMSMap.Hand = NMSMap.Hand.MAIN,
        width: Int = 128,
        height: Int = 128,
        builder: ItemBuilder.() -> Unit = {}
    )

    /**
     * 给玩家构建并发送地图
     *
     * @param file 图片文件
     * @param hand 手
     * @param width 宽度
     * @param height 高度
     * @param builder 物品构建器
     */
    fun Player.sendMap(
        file: File,
        hand: NMSMap.Hand = NMSMap.Hand.MAIN,
        width: Int = 128,
        height: Int = 128,
        builder: ItemBuilder.() -> Unit = {}
    )

    /**
     * 给玩家构建并发送地图
     *
     * @param image 缓冲区图像
     * @param hand 手
     * @param width 宽度
     * @param height 高度
     * @param builder 物品构建器
     */
    fun Player.sendMap(
        image: BufferedImage,
        hand: NMSMap.Hand = NMSMap.Hand.MAIN,
        width: Int = 128,
        height: Int = 128,
        builder: ItemBuilder.() -> Unit = {}
    )