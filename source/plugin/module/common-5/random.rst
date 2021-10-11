==========
权重随机器
==========

在多个含有权重的元素中随机选取，具体表现在 ``taboolib.common5.RandomList`` 类中。使用方式如下：

.. code-block:: kotlin

    // 定义随机列表
    val random = RandomList(Material.IRON_INGOT to 1, Material.GOLD_INGOT to 5)
    // 添加
    random.add(Material.DIAMOND to 10)
    // 获取
    val material = random.random()!!