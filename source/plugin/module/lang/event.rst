======
事件
======

该模块有 2 个事件，它们是:

* PlayerSelectLocaleEvent
* SystemSelectLocaleEvent

它们都是不可取消的

.. code-block:: kotlin

    /**
     * 玩家选择语言地区事件
     *
     * @param player 玩家
     * @param locale 语言地区（例如：zh_CN）
     */
    class PlayerSelectLocaleEvent(val player: ProxyPlayer, var locale: String) : ProxyEvent() {

        override val allowCancelled: Boolean
            get() = false
    }

    /**
     * 系统选择语言地区事件
     *
     * @param locale 语言地区（例如：zh_CN）
     */
    class SystemSelectLocaleEvent(var locale: String) : ProxyEvent() {

        override val allowCancelled: Boolean
            get() = false
    }