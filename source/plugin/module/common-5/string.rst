==========
字符串工具
==========

关于字符串的部分工具，具体表现为以下顶级或扩展函数：

.. code-block:: kotlin

    /**
     * 将字符串通过特定规范转换为毫秒
     * 输入: 1h30m
     * 输出: 5400000
     * 支持单位: d,h,m,s
     */
    fun String.parseMillis(): Long

    /**
     * 将文字转换为打印机特效，并忽略颜色代码
     * 输入: 我是脑瘫
     * 输出: [我, 我是, 我是脑, 我是脑瘫]
     */
    fun String.printed(separator: String = ""): List<String>

    /**
     * 生成百分比进度条
     * 输入: createBar("0", "@", 10, 0.5)
     * 输出: @@@@@00000
     *
     * @param empty 空
     * @param fill 填充
     * @param length 长度
     * @param percent 百分比
     */
    fun createBar(empty: String, fill: String, length: Int, percent: Double): String