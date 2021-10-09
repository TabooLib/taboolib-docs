=====
随机
=====

关于集合的部分工具，具体表现为以下顶级函数：

.. code-block:: kotlin

    /**
     * 通过 ThreadLocalRandom 生成 Random
     */
    fun random(): Random

    /**
     * 通过 ThreadLocalRandom 生成 0 ~ v 之间的随机浮点数
     */
    fun random(v: Double): Boolean

    /**
     * 通过 ThreadLocalRandom 生成 0 ~ v 之间的随机整型数
     */
    fun random(v: Int): Int
    
    /**
     * 通过 ThreadLocalRandom 生成 num1 ~ num2 之间的随机整型数
     */
    fun random(num1: Int, num2: Int): Int

    /**
     * 通过 ThreadLocalRandom 生成 num1 ~ num2 之间的随机浮点数
     */
    fun random(num1: Double, num2: Double): Double