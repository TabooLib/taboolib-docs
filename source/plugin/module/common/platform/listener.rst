=======
监听器
=======

每个平台都有监听器（Listener）部分，但 TabooLib 自身不处理监听器。本文所描述的内容仅限监听器的运用，事件的定义请参考 :doc:`event` 部分。

注册监听器
~~~~~~~~~

任何平台的事件都通过同样的方式注册。基于 :doc:`/plugin/inject`，监听器需要在单例或伴生类中定义。

.. code-block:: kotlin

    object MyListener {
        
        /**
         * 监听器仅接受一个参数，为事件的类型
         */
        @SubscribeEvent
        fun e(e: PlayerJoinEvent) {
            e.player.sendMessage("HelloWorld")
        }
    }

不需要实现任何接口以及添加多余的注解，一步到位。

在 ``@SubscribeEvent`` 的属性中包含了各个平台所需要的监听器参数，具体表现为：

**Bukkit, Nukkit**

.. csv-table::
    :header: "属性", "作用", "示例"
    :widths: 1, 1, 1

    "priority", "优先级", "EventPriority.NORMAL"
    "ignoreCancelled", "忽略已被取消的事件", "false"

**BungeeCord**

.. csv-table::
    :header: "属性", "作用", "示例"
    :widths: 1, 1, 1

    "level", "优先级", "0"
    "ignoreCancelled", "忽略已被取消的事件", "false"

**Velocity**

.. csv-table::
    :header: "属性", "作用", "示例"
    :widths: 1, 1, 1

    "postOrder", "优先级", "PostOrder.NORMAL"

**Sponge 7/8**

.. csv-table::
    :header: "属性", "作用", "示例"
    :widths: 1, 1, 1

    "order", "优先级", "EventOrder.DEFAULT"
    "beforeModifications", "在其他服务器修改前调用监听器", "false"

可能不存在的事件
~~~~~~~~~~~~~~

假设我们监听了第三方插件中的事件，若这个插件并未安装，那么就会导致整个类无法加载。但往往很多时候，我们不会使用 ``depend`` 来解决这个问题。在 TabooLib 中我们可以使用 ``OptionalEvent`` 事件来代替。

在 Bukkit 1.8 没有副手也没有 ``PlayerSwapHandItemsEvent`` 事件，直接监听会导致插件无法在 1.8 版本使用。

.. code-block:: kotlin

    @SubscribeEvent(bind = "org.bukkit.event.player.PlayerSwapHandItemsEvent")
    fun onSwap(ope: OptionalEvent) {
        val e = ope.get<PlayerSwapHandItemsEvent>()
        // ...
    }

使用 ``bind`` 属性指向完整的类名，即可定义一个 **可能不存在的事件**，同等于直接监听。