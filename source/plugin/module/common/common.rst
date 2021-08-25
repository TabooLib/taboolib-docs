========
程序入口
========

TabooLibCommon 作为 TabooLib 的入口，用于部署运行环境以及调度生命周期，但是这些方法不需要由插件开发者调用。除此之外该类还提供了一些必要的方法。

.. code-block:: java

    /**
     * 用于测试的快速启动方法，同 lifeCycle
     * 会按顺序触发 CONST、INIT、LOAD、ENABLE 生命周期
     */
    public static void testSetup()

    /**
     * 用于测试的快速注销方法，同 lifeCycle
     * 会触发 DISABLE 生命周期
     */
    public static void testCancel()

    /**
     * 生命周期
     * 不依赖于任何平台
     */
    public static void lifeCycle(LifeCycle lifeCycle)

    /**
     * 生命周期
     * 依赖于任意平台的生命周期的启动或卸载方法
     */
    public static void lifeCycle(LifeCycle lifeCycle, @Nullable Platform platform)

    /**
     * 当前是否存在 Kotlin 运行环境
     */
    public static boolean isKotlinEnvironment()

    /**
     * 当前运行平台
     */
    @NotNull
    public static Platform getRunningPlatform()

    /**
     * 是否停止 TabooLib 及插件加载流程
     */
    public static boolean isStopped()

    /**
     * 停止 TabooLib 及插件加载流程
     */
    public static void setStopped(boolean value)

.. warning::

    正常情况下，该类中有关于 ``lifeCycle`` 的方法禁止手动调用。但如果您的项目不依赖任何 Minecraft 平台，可以参考下面的方式来启动 TabooLib 服务。

.. code-block:: java

    import taboolib.common.TabooLibCommon;

    public class Application {

        public static void main(String[] args) {
            // 快速启动
            TabooLibCommon.testSetup();
            Service.run();
        }
    }
