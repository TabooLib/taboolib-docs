=========
依赖注入
=========

TabooLib 使用 **侵入式** 依赖注入（Dependency Injection）的方式向插件提供服务，指 TabooLib 会主动的向插件中的所有单例（object）或伴生类（companion object）中进行检查和注入工作。例如绑定一些方法或赋值 API 实例。

.. code-block:: kotlin

    package io.github.username.project

    import taboolib.common.platform.*
    import taboolib.module.configuration.Config
    import taboolib.module.configuration.SecuredFile
    import org.bukkit.event.player.PlayerJoinEvent

    object ExampleLifeCycle {

        @Config
        lateinit var conf: SecuredFile
            private set

        @Awake(LifeCycle.ENABLE)
        fun enable() {
            println("Successfully running ExamplePlugin!")
        }

        @SubscriptEvent
        fun fun(PlayerJoinEvent e) {
            // ...   
        }
    }

