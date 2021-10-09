========
集合相关
========

关于集合的部分工具，具体表现为以下顶级或扩展函数：

.. code-block:: kotlin

    /**
     * 获取列表中特定范围内的元素
     * 
     * @param list 列表
     * @param start 开始位置
     * @param end 结束位置（默认为元素数量）
     */
    fun <T> subList(list: List<T>, start: Int = 0, end: Int = list.size): List<T>

    /**
     * 获取 Map 中特定范围内的元素
     * 
     * @param map Map
     * @param start 开始位置
     * @param end 结束位置（默认为元素数量）
     */
    fun <K, V> subMap(map: Map<K, V>, start: Int = 0, end: Int = map.size - 1): List<Map.Entry<K, V>>

    /**
     * 安全的写入元素
     *
     * @param index 下标
     * @param element 元素
     * @param def 若写入位置之前存在空缺，则写入该默认值
     */
    fun <T> MutableList<T>.setSafely(index: Int, element: T, def: T)

    /**
     * 安全的插入元素
     *
     * @param index 下标
     * @param element 元素
     * @param def 若插入位置之前存在空缺，则写入该默认值
     */
    fun <T> MutableList<T>.addSafely(index: Int, element: T, def: T)

    /**
     * 遍历一个集合
     * 可以在遍历的过程中使用 close() 方法结束遍历，以弥补 Kotlin 无法使用 break 的设计
     *
     * @param start 开始位置（可省略）
     * @param end 结束位置（可省略）
     * @param reversed 是否逆向
     * @param action 方法体
     * @return 最后一次方法体执行结果
     */
    fun <T, C : Iterable<T>, R> C.each(start: Int = -1, end: Int = -1, reversed: Boolean = false, action: Closeable.(index: Int, T) -> R?): R?

