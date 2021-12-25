==========
进度
==========

关于进度的工具，该工具只适用于1.13及以上游戏版本

**具体表现为以下扩展函数：**

.. code-block:: kotlin

    /**
     * 发送虚拟 Toast 成就信息
     *
     * @param icon 图标
     * @param message 信息
     * @param frame 成就框架
     * @param background 成就背景图片
     */
    fun Player.sendToast(icon: Material, message: String, frame: ToastFrame = ToastFrame.TASK, background: ToastBackground = ToastBackground.ADVENTURE)

    /**
     * 成就框架枚举
     *
     * TASK 条目
     * GOAL 目标
     * CHALLENGE 挑战
     */
    enum class ToastFrame {
        TASK,GOAL,CHALLENGE
    }

    /**
     * 成就背景图片枚举
     *
     * @param url 地址
     * ADVENTURE 冒险
     * END 末地之路
     */
    enum class ToastBackground(val url: String) {
        ADVENTURE("minecraft:textures/gui/advancements/backgrounds/adventure.png"),
        END("minecraft:textures/gui/advancements/backgrounds/end.png")
    }