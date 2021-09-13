=====
事件
=====

每个平台都有事件（Event）部分，但 TabooLib 自身不处理事件。本文所描述的内容仅限事件的定义，实际运用请参考 :doc:`listener` 部分。

跨平台事件
~~~~~~~~~

跨平台事件指使用 TabooLib 提供的接口定义的事件可以在多个平台中使用，具体表现为：

.. code-block:: kotlin

    class SomethingEvent(val proxyPlayer: ProxyPlayer): ProxyEvent {
        
        /**
         * 事件是否允许被取消，默认为 true
         * 尝试取消 allowCancelled 为 false 的事件会抛出 IllegalStateException 异常
         */
        override val allowCancelled: Boolean
            get() = false
    }

唤起事件：

.. code-block:: kotlin

    // call 方法的返回值 Boolean 表示这个事件是否被取消
    SomethingEvent(proxyPlayer).call()

.. warning::

    依赖于 ``ProxyEvent`` 的跨平台事件，只能被 TabooLib 开发的插件监听。

子平台事件
~~~~~~~~~

并非所有开发者都喜欢使用 TabooLib，因此我们可以使用子平台事件。但是相对的，子平台事件是基于平台的，无法跨平台应用。

.. csv-table::
    :header: "平台", "对应事件"
    :widths: 1, 2

    "Bukkit", "BukkitProxyEvent"
    "Nukkit", "NukkitProxyEvent"
    "BungeeCord", "BungeeProxyEvent"
    "Sponge (api-7)", "Sponge7ProxyEvent"
    "Sponge (api-8)", "Sponge8ProxyEvent"
    "Velocity", "VelocityProxyEvent"

子平台事件的使用方式与 ``ProxyEvent`` 无异。

.. code-block:: kotlin

    class SomethingEvent(val player: Player): BukkitProxyEvent

使用子平台事件需要安装对应的平台模块，例如 ``BukkitProxyEvent`` 需要安装 ``platfom-bukkit``。