==========
物品 NBT
==========

关于 NBT 的部分工具，具体表现为以下顶级或扩展函数：

物品堆NBT
~~~~~~~~

.. code-block:: kotlin

    /**
     * 获取物品的NBT数据
     */
    fun ItemStack.getItemTag(): ItemTag

    /**
     * 写入物品的NBT数据
     *
     * @param itemTag NBT
     * @return 物品堆
     */
    fun ItemStack.setItemTag(itemTag: ItemTag): ItemStack

处理NBT数据
~~~~~~~~

.. code-block:: kotlin

    /**
     * 获取NBT
     *
     * @param key 键
     * @return NBT数据
     */
    fun get(key: Any): ItemTagData

    /**
     * 获取NBT若为空返回默认值
     *
     * @param key 键
     * @param base 默认值
     * @return NBT数据
     */
    fun getOrElse(key: String, base: ItemTagData): ItemTagData

    /**
     * 获取节点NBT
     *
     * @param key 节点 如"taboolib.id"
     * @return NBT数据
     */
    fun getDeep(key: String): ItemTagData

    /**
     * 获取节点NBT若为空返回默认值
     *
     * @param key 节点 如"taboolib.id"
     * @param base 默认值
     * @return NBT数据
     */
    fun getDeepOrElse(key: String, base: ItemTagData): ItemTagData

    /**
     * 设置NBT
     *
     * @param key 键
     * @param value 值
     * @return NBT数据
     */
    fun put(key: String, value: Any): ItemTagData

    /**
     * 设置节点NBT
     *
     * @param key 节点 如"taboolib.id"
     * @param value 值
     * @return NBT数据
     */
    fun putDeep(key: String, value: Any): ItemTagData

    /**
     * 删除NBT
     *
     * @param key 键
     * @return NBT数据
     */
    fun remove(key: String): ItemTagData

    /**
     * 删除节点NBT
     *
     * @param key 节点 如"taboolib.id"
     * @return NBT数据
     */
    fun removeDeep(key: String): ItemTagData