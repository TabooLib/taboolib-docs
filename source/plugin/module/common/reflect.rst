=====
反射
=====

本篇内容具体表现在以下顶级函数：

.. code-block:: kotlin

    /**
     * 已注册的 ReflexRemapper
     * 直接添加到改容器即可完成注册，起初用于转换 1.17 版本的混淆字段名称
     */
    val remapper = ArrayList<ReflexRemapper>()

    /**
     * 不通过构造函数实例化对象
     */
    fun <T> Class<T>.unsafeInstance(): Any

    /**
     * 通过构造方法实例化对象
     */
    fun <T> Class<T>.invokeConstructor(vararg parameter: Any?): T

    /**
     * 执行方法
     * @param name 方法名称
     * @param parameter 方法参数
     * @param fixed 是否为静态方法
     */
    fun <T> Any.invokeMethod(name: String, vararg parameter: Any?, fixed: Boolean = false): T?

    /**
     * 获取字段
     * @param path 字段名称，使用 "/" 符号进行递归获取
     * @param fixed 是否为静态字段
     */
    fun <T> Any.getProperty(path: String, fixed: Boolean = false): T?

    /**
     * 修改字段
     * @param path 字段名称，使用 "/" 符号进行递归获取
     * @param value 值
     * @param fixed 是否为静态字段
     */
    fun Any.setProperty(path: String, value: Any?, fixed: Boolean = false)

无论是对于方法还是字段的反射，都会缓存并对所有父类及接口进行递归检查。了解过 Bukkit 逆向的同学参考以下代码。

.. code-block:: kotlin

    // 获取 CraftPlayer 中的 entity 字段，并继续获取 locale 字段。
    player.getProperty<String>("entity/locale")