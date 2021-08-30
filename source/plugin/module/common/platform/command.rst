=====
命令
=====

.. tips::

    本篇内容不限于某个类或方法，而是多个内容组成的一套系统。

通过 TabooLib 提供的接口，一次编写的命令可以在各个平台上使用，具体表现为：

.. code-block:: kotlin

    command("tpuuid") {
        literal("random") {
            execute<ProxyPlayer> { player, _, _ ->
                player.teleport(player.entities().randomOrNull() ?: return@execute)
            }
        }
        dynamic(optional = true) {
            suggestion<ProxyPlayer> { player, _ ->
                player.entities().map { it.toString() }
            }
            execute<ProxyPlayer> { player, _, argument ->
                player.teleport(UUID.fromString(argument))
            }
        }
        execute<ProxyPlayer> { player, _, _ ->
            player.teleport(player.entityNearly() ?: return@execute)
        }
    }

或是：

.. code-block:: kotlin

    @CommandHeader("tpuuid")
    class TpUUID {

        @CommandBody
        val main = mainCommand {
            dynamic(optional = true) {
                suggestion<ProxyPlayer> { player, _ ->
                    player.entities().map { it.toString() }
                }
                execute<ProxyPlayer> { player, _, argument ->
                    player.teleport(UUID.fromString(argument))
                }
            }
            execute<ProxyPlayer> { player, _, _ ->
                player.teleport(player.entityNearly() ?: return@execute)
            }
        }

        @CommandBody
        val random = subCommand {
            execute<ProxyPlayer> { player, _, _ ->
                player.teleport(player.entities().randomOrNull() ?: return@execute)
            }
        }
    }

标准命令注册
~~~~~~~~~~~

通过顶级函数 ``command`` 进行命令注册，该函数中除命令名称外的其他参数均为可选。

.. code-block:: kotlin

    command("command") {
        
    }

简化命令注册
~~~~~~~~~~~