======
事件
======

该模块有 2 个事件，它们是:

* PlayerSelectLocaleEvent
* SystemSelectLocaleEvent

它们都是不可取消的

.. code-block:: kotlin

/**
 * 玩家选择地区事件
 *
 * @param player 玩家
 * @param locale 地区
 */
class PlayerSelectLocaleEvent(val player: ProxyPlayer, var locale: String) : ProxyEvent() {

    override val allowCancelled: Boolean
        get() = false
}

/**
 * 系统选择地区事件
 *
 * @param locale 地区
 */
class SystemSelectLocaleEvent(var locale: String) : ProxyEvent() {

    override val allowCancelled: Boolean
        get() = false
}