====
IO
====

本篇内容具体表现在以下顶级函数：

.. code-block:: kotlin

    /**
     * 获取当前插件名称
     */
    val pluginId: String

    /**
     * 获取当前插件版本
     */
    val pluginVersion: String

    /**
     * 当前是否在主线程中运行
     */
    val isPrimaryThread: Boolean

    /**
     * 获取控制台对象
     * 例如：
     * server<ConsoleCommandSender>()
     */
    fun <T> server(): T

    /**
     * 打印日志
     */
    fun info(vararg message: Any?)

    /**
     * 打印错误日志
     */
    fun severe(vararg message: Any?)

    /**
     * 打印警告日志
     */
    fun warning(vararg message: Any?)

    /**
     * 释放当前插件内的特定资源文件
     * @param replace 是否覆盖文件
     */
    fun releaseResourceFile(path: String, replace: Boolean = false): File

    /**
     * 获取当前插件的 Jar 文件对象
     */
    fun getJarFile(): File

    /**
     * 获取当前插件的配置文件目录
     * 可能不存在，需要手动调用 mkdirs 方法创建
     */
    fun getDataFolder(): File

    /**
     * 获取当前平台的信息
     * 用于 BStats 统计，无实际用途
     */
    fun getPlatformData(): Map<String, Any>