=====
角色
=====

.. tips::

    本篇内容不限于某个类或方法，而是多个内容组成的一套系统。

角色是 TabooLib 用于应对各个平台中 **玩家** 及 **命令发送者** 的解决方案，具体表现为：

* taboolib.common.platform.ProxyPlayer
* taboolib.common.platform.ProxyCommandSender

其中的属性与方法还原自 Bukkit 平台，主要目的则是在跨平台接口中代表对应的平台实现。

.. csv-table::
    :header: "平台", "ProxyPlayer 实现", "ProxyCommandSender 实现"
    :widths: 1, 3, 3

    "Bukkit", "Player", "CommandSender"
    "Nukkit", "Player", "CommandSender"
    "BungeeCord", "ProxiedPlayer", "CommandSender"
    "Sponge (api-7)", "Player", "CommandSource"
    "Sponge (api-8)", "ServerPlayer", "Audience"
    "Velocity", "Player", "CommandSource"

通过以下方式将 Proxy 类型转换为具体的平台类型。

.. code-block:: kotlin

    val proxyPlayer: ProxyPlayer = ...
    // 转换为 Bukkit 类型
    val player = player.cast<Player>()

顶级函数
~~~~~~~~

.. code-block:: kotlin

    /**
     * 获取控制台
     */
    fun console(): ProxyCommandSender

    /**
     * 将平台实现转换为跨平台实现
     * 例如：
     * adaptCommandSender(Bukkit.getConsoleCommandSender())
     */
    fun adaptCommandSender(any: Any): ProxyCommandSender

    /**
     * 获取所有在线玩家
     */
    fun onlinePlayers(): List<ProxyPlayer>

    /**
     * 将平台实现转换为跨平台实现
     * 例如：
     * adaptPlayer(Bukkit.getOnlinePlayer("Steve"))
     */
    fun adaptPlayer(any: Any): ProxyPlayer

    /**
     * 通过名称获取玩家
     */
    fun getProxyPlayer(name: String): ProxyPlayer?

    /**
     * 通过 UUID 获取玩家
     */
    fun getProxyPlayer(uuid: UUID): ProxyPlayer?

.. tips::

    这些方法可以在任何位置使用。