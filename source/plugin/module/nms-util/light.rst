===========
光照
===========

关于方块光照的工具，该工具只适用于1.12及以上游戏版本

**具体表现为以下扩展函数：**

.. code-block:: kotlin

    /**
     * 创建光源
     *
     * @param lightLevel 光照等级
     * @param lightType 光源类型
     * @param update 是否更新区块光照
     * @param viewers 可见玩家
     */
    fun Block.createLight(
        lightLevel: Int,
        lightType: LightType = LightType.ALL,
        update: Boolean = true,
        viewers: Collection<Player> = Bukkit.getOnlinePlayers()
    ): Boolean

    /**
     * 删除光源
     *
     * @param lightType 光源类型
     * @param update 是否更新区块光照
     * @param viewers 可见玩家
     */
    fun Block.deleteLight(
        lightType: LightType = LightType.ALL,
        update: Boolean = true,
        viewers: Collection<Player> = Bukkit.getOnlinePlayers(),
    ): Boolean