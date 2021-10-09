========
项目相关
========

关于 TabooLib 项目的部分工具，具体表现为以下顶级或扩展函数：

.. code-block:: kotlin

    /**
     * 当前插件的所有类
     */
    val runningClasses: List<Class<*>>

    /**
     * 取该类在当前项目中被加载的任何实例
     * 例如：@Awake 自唤醒类，或是 Kotlin Companion Object、Kotlin Object 对象
     * @param newInstance 若无任何已加载的实例，是否实例化
     */
    fun <T> Class<T>.getInstance(newInstance: Boolean = false): Supplier<T>?
    
    /**
     * 依赖注入
     */
    fun <T> Class<T>.inject()

    /**
     * 获取该类所对应的平台实现（@PlatformSide）
     */
    fun <T> Class<T>.findImplementation(): T?

    /**
     * 通过 URL 获取类文件
     * 该方法将会进行 IO 操作，且不通过任何缓存
     */
    fun URL.getClasses(): List<Class<*>>

    /**
     * 获取当前项目的 groupId
     */
    inline val groupId: String

    /**
     * 获取 "taboolib" 字符串
     * 若在项目中显示声明 "taboolib" 将会被重定向，故添加此方法
     */
    inline val taboolibId: String
    
    /**
     * 同等于：
     * groupId + taboolibId
     */
    inline val taboolibPath: String