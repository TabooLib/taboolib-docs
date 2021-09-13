===========
插件生命周期
===========

在不通过特殊手段操控插件时，我们大可认为是游戏阶段的变化。每个平台都有其自己的生命周期规范，在 TabooLib 中我们规定了统一的写法。但是这种统一的写法并不能涵盖所有平台的生命周期，所以在有特殊需求的情况下，依旧使用原平台的方法。

生命周期阶段
~~~~~~~~~~~

**CONST**

当插件主类初始化时。此时插件的构造方法未执行，主类还不存在实例。

**INIT**

当插件主类的实例被构造时。此时可以调用插件实例，以及所有注入工作完成。

**LOAD**

对应主类 ``onLoad()`` 方法，当插件开始加载时。此时不同平台开始出现差异。

.. csv-table::
   :header: "平台", "对应"
   :widths: 1, 2
   
   "bukkit, nukkit, bungee", "对应原 ``onLoad()`` 方法"
   "sponge-api7", "对应原 ``GamePreInitializationEvent`` 事件"
   "sponge-api8", "对应原 ``ConstructPluginEvent`` 事件"
   "velocity", "对应原 ``ProxyInitializeEvent`` 事件"
 
 
**ENABLE**

对应主类 ``onEnable()`` 方法，当插件开始启动时。你应该在这个事件下完成插件的所有准备工作，例如命令注册。

.. csv-table::
   :header: "平台", "对应"
   :widths: 1, 2
   
   "bukkit, nukkit, bungee", "对应原 ``onEnable()`` 方法"
   "sponge-api7", "对应原 ``GameInitializationEvent`` 事件"
   "sponge-api8", "对应原 ``StartingEngineEvent<Server>`` 事件"
   "velocity", "对应原 ``ProxyInitializeEvent`` 事件，与 LOAD 同时执行"

**ACTIVE**

对应主类 ``onActive()`` 方法，当服务器完全启动时。此时调度器开始执行。

.. csv-table::
   :header: "平台", "对应"
   :widths: 1, 2
   
   "bukkit, nukkit, bungee, velocity", "对应调度器开始执行时"
   "sponge-api7", "对应原 ``GameStartedServerEvent`` 事件"
   "sponge-api8", "对应原 ``StartedEngineEvent<Server>`` 事件"

**DISABLE**

对应主类 ``onDisable()`` 方法，当插件卸载时。

.. csv-table::
   :header: "平台", "对应"
   :widths: 1, 2
   
   "bukkit, nukkit, bungee", "对应原 ``onDisable()`` 方法"
   "sponge-api7", "对应原 ``GameStoppedServerEvent`` 事件"
   "sponge-api8", "对应原 ``StoppingEngineEvent<Server>`` 事件"
   "velocity", "对应原 ``ProxyShutdownEvent`` 事件"


生命周期方法
~~~~~~~~~~~~

除了在主类继承对应的生命周期方法外，你还可以在其他任何单例中使用 ``@Awake`` 注解来绑定生命周期方法。详见 :doc:`inject` 部分。
  
.. code-block:: kotlin

    package io.github.username.project

    import taboolib.common.platform.Plugin
    import taboolib.common.platform.Awake

    object ExampleLifeCycle {

        @Awake(LifeCycle.ENABLE)
        fun enable() {
            println("Successfully running ExamplePlugin!")
        }
    }

.. note::
  
    每个生命周期阶段所绑定的方法只会执行一次。

.. warning::

    所有注入工作只允许在单例 (object) 或伴生对象 (companion object) 中完成。
    
若要阻止其他插件引用可以使用 ``internal object``，禁止使用 ``private object``。

生命周期跳过
~~~~~~~~~~~~

使用 ``@SkipTo`` 注解可以跳过某个生命周期，来避免静态代码块在预期外被调用。来看下面这段报错。

.. code-block:: none

    [21:56:20 INFO]: Loading libraries, please wait...
    [21:56:23 INFO]: class cc.maxmc.maxmfa.data.PlayerData$Companion
    [21:56:23 WARN]: java.lang.ExceptionInInitializerError
    [21:56:23 WARN]: 	at java.base/java.lang.Class.forName0(Native Method)
    [21:56:23 WARN]: 	at java.base/java.lang.Class.forName(Class.java:375)
    [21:56:23 WARN]: 	at cc.maxmc.maxmfa.taboolib.common.io.Project1Kt.getInstance(Project1.kt:35)
    [21:56:23 WARN]: 	at cc.maxmc.maxmfa.taboolib.common.inject.RuntimeInjector.inject(RuntimeInjector.java:87)
    [21:56:23 WARN]: 	at cc.maxmc.maxmfa.taboolib.common.inject.RuntimeInjector.injectAll(RuntimeInjector.java:65)
    [21:56:23 WARN]: 	at cc.maxmc.maxmfa.taboolib.common.TabooLibCommon.lifeCycle(TabooLibCommon.java:95)
    [21:56:23 WARN]: 	at cc.maxmc.maxmfa.taboolib.platform.BukkitPlugin.<clinit>(BukkitPlugin.java:34)
    [21:56:23 WARN]: 	at java.base/java.lang.Class.forName0(Native Method)
    [21:56:23 WARN]: 	at java.base/java.lang.Class.forName(Class.java:466)
    [21:56:23 WARN]: 	at org.bukkit.plugin.java.PluginClassLoader.<init>(PluginClassLoader.java:64)
    [21:56:23 WARN]: 	at org.bukkit.plugin.java.JavaPluginLoader.loadPlugin(JavaPluginLoader.java:131)
    [21:56:23 WARN]: 	at org.bukkit.plugin.SimplePluginManager.loadPlugin(SimplePluginManager.java:329)
    [21:56:23 WARN]: 	at org.bukkit.plugin.SimplePluginManager.loadPlugins(SimplePluginManager.java:251)
    [21:56:23 WARN]: 	at org.bukkit.craftbukkit.v1_8_R3.CraftServer.loadPlugins(CraftServer.java:292)
    [21:56:23 WARN]: 	at net.minecraft.server.v1_8_R3.DedicatedServer.init(DedicatedServer.java:198)
    [21:56:23 WARN]: 	at net.minecraft.server.v1_8_R3.MinecraftServer.run(MinecraftServer.java:525)
    [21:56:23 WARN]: 	at java.base/java.lang.Thread.run(Thread.java:831)
    [21:56:23 WARN]: Caused by: java.lang.NullPointerException
    [21:56:23 WARN]: 	at org.jetbrains.exposed.dao.EntityClass.<init>(EntityClass.kt:19)
    [21:56:23 WARN]: 	at org.jetbrains.exposed.dao.UUIDEntityClass.<init>(UUIDEntity.kt:9)
    [21:56:23 WARN]: 	at org.jetbrains.exposed.dao.UUIDEntityClass.<init>(UUIDEntity.kt:9)
    [21:56:23 WARN]: 	at cc.maxmc.maxmfa.data.PlayerData$Companion.<init>(ExposedDataStorage.kt:92)
    [21:56:23 WARN]: 	at cc.maxmc.maxmfa.data.PlayerData$Companion.<init>(ExposedDataStorage.kt)
    [21:56:23 WARN]: 	at cc.maxmc.maxmfa.data.PlayerData.<clinit>(ExposedDataStorage.kt:95)
    [21:56:23 WARN]: 	... 17 more

报错的源头在 ``cc.maxmc.maxmfa.data.PlayerData.<clinit>`` 也就是静态代码块部分，且产生的过程为 ``lifeCycle`` -> ``injectAll`` -> ``inject``。那么我们由此得出该报错因侵入式依赖注入导致。

在 ``CONST`` 生命周期下，TabooLib 会检查插件中的每个类的属性和方法，因此导致静态代码块被执行。我们可以添加 ``@SkipTo`` 注解来避免这类问题发生。

.. code-block:: kotlin

    @SkipTo(LifeCycle.ENABLE)
    object ExposedDataStorage

如果是伴生类则需要：

.. code-block:: kotlin

    @SkipTo(LifeCycle.ENABLE)
    companion object

在 ``ENABLE`` 生命周期前不对该类执行任何侵入式行为。