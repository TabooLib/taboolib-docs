=============
Linked（多页）
=============


此工具可以被用于制作 **商城、仓库** 等插件的快捷界面构建工具

基本使用方法
========

.. code-block:: kotlin

    Player.openMenu<Linked<物品类型>>(标题){
        // 界面应该显示几行
        rows(行数)
        // 可放置物品位置，这个地方应该提供一个MutableList<Int>的列表
        slots(mutableListOf().toList())
        // 显示在界面上的所有元素集合
        elements {
            ...
        }
        // 显示的物品，你可能传入的是一个实体类，但是至少应该有可以表示ItemStack的一个属性
        onGenerate { player, element, index, slot ->
            ...
        }
        // 下一页位置以及物品
        setNextPage(位置) { page, hasNextPage ->
            // 如果有下一页
            if (hasNextPage) {
                ...
            } else {
                ...
            }
        }
        // 上一页位置以及物品
        setPreviousPage(位置) { page, hasPreviousPage ->
            // 如果有上一页
            if (hasPreviousPage) {
                ...
            } else {
                ...
            }
        }
        // 设置按钮以及点击之后触发的事件
        set(位置, 物品) {
            // 点击之后执行的逻辑
            ...
        }
        // 点击上半部分触发
        onClick { event, element ->
            // 点击之后执行的逻辑
            ...
        }
        // 点击任意地方触发
        onClick { it ->
            // 点击之后执行的逻辑
            ...
        }
        // 关闭之后的动作
        onClose {
            // 关闭后执行的逻辑
            ...
        }
    }
