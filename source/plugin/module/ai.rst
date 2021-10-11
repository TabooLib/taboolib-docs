===========
module-ai
===========

这部分作为 Bukkit 平台下实现自定义生物寻路（Pathfinder）以及相关控制方法。

**该模块依赖于：**

* common
* module-nms

**安装方式如下所示：**

.. code-block:: kotlin

    taboolib {
        install("common", "module-nms", "module-ai")
    }

在开始前，请您阅读 `[上古之石]Pathfinder插件教程 <https://www.mcbbs.net/thread-775757-1-1.html>`_ 以确保您大致了解原版 Pathfinder 的实现逻辑。

在该模块中，由 ``taboolib.module.ai.SimpleAi`` 代替了 PathfinderGoal 类。

.. code-block:: kotlin

    /**
     * 使用 SimpleAi 实现上方教程中提到的蜘蛛生成网生成AI
     */
    class PathfinderGoalNet(val spider: Spider) : SimpleAi() {

        override fun shouldExecute(): Boolean {
            if (random(10) != 0) {
                return false
            }
            if (!spider.isOnGround) {
                return false
            }
            return true
        }

        override fun continueExecute(): Boolean {
            return false
        }

        /**
         * 等价于 startExecute() 方法
         */        
        override fun startTask() {
            spider.location.block.type = Material.COBWEB
        }
    }

随后使用扩展函数注册AI：

.. code-block:: kotlin

    val spider: Spider = ...
    spider.addGoalAi(PathfinderGoalNet(spider), 1)

其余控制方法表现在以下扩展函数：

.. code-block:: kotlin

    fun LivingEntity.addGoalAi(ai: SimpleAi, priority: Int)

    fun LivingEntity.addTargetAi(ai: SimpleAi, priority: Int)

    fun LivingEntity.replaceGoalAi(ai: SimpleAi, priority: Int)

    fun LivingEntity.replaceTargetAi(ai: SimpleAi, priority: Int)
    
    /**
     * 根据类的 simpleName 属性替换一个 AI
     */
    fun LivingEntity.replaceGoalAi(ai: SimpleAi, priority: Int, name: String?)

    fun LivingEntity.replaceTargetAi(ai: SimpleAi, priority: Int, name: String?)

    fun LivingEntity.removeGoalAi(priority: Int)

    fun LivingEntity.removeTargetAi(priority: Int)

    /**
     * 根据类的 simpleName 属性移除一个 AI
     */
    fun LivingEntity.removeGoalAi(name: String)

    fun LivingEntity.removeTargetAi(name: String)

    fun LivingEntity.clearGoalAi()

    fun LivingEntity.clearTargetAi()

    fun LivingEntity.getGoalAi(): Iterable<*>

    fun LivingEntity.getTargetAi(): Iterable<*>

    fun LivingEntity.setGoalAi(ai: Iterable<*>)

    fun LivingEntity.setTargetAi(ai: Iterable<*>)

    /**
     * 使用原版 Navigation 移动实体到特定坐标
     */
    fun LivingEntity.navigationMove(location: Location, speed: Double = 0.2): Boolean

    /**
     * 使用原版 Navigation 移动实体到特定实体位置
     */
    fun LivingEntity.navigationMove(target: LivingEntity, speed: Double = 0.2): Boolean

    fun LivingEntity.navigationReach(): Boolean

    fun LivingEntity.controllerLookAt(target: Location)

    fun LivingEntity.controllerLookAt(target: Entity)

    fun LivingEntity.controllerJumpReady()

    fun LivingEntity.controllerJumpCurrent(): Boolean