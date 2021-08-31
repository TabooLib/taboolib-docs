=====
命令
=====

.. tips::

    本篇内容不限于某个类或方法，而是多个内容组成的一套系统。

每个平台都有命令（Command）部分，通过 TabooLib 提供的接口，一次编写的命令可以在各个平台上使用，具体表现为：

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

    // 注册 command 命令
    command("command") {
        
    }
    // 注册 command 命令并添加别名与描述
    command("command", aliases = listOf("cmd"), description = "A command") {

    }

**可用参数列表**

.. csv-table::
    :header: "名称", "作用"
    :widths: 1, 2

    "aliases", "别名"
    "description", "描述"
    "usage", "使用方式"
    "permission", "使用权限（默认为：插件名称.指令.use）"
    "permissionMessage", "没有权限的提示信息",
    "permissionDefault", "默认拥有权限（该功能目前仅限 Bukkit 平台）"

TabooLib 到命令注册与 Bukkit 不同，没有 ``args`` 的概念，而是通过逐层的嵌套来完成对命令的解释。

.. code-block:: kotlin

    command("command") {
        execute<ProxyCommandSender> { sender, context, argument ->
            sender.sendMessage("HelloWorld")
        }
    }

可以看到这个命令只有一层，用户在输入 ``/command`` 时得到提示 ``HelloWorld``。

.. warning::

    命令的逻辑必须在 ``execute`` 代码块中实现。

接下来需要实现 ``/command [玩家]`` 命令向该玩家发送 ``HelloWorld`` 信息。

.. code-block:: kotlin

    command("command") {
        // 二级参数入口。玩家名称是不固定的，所以使用 dynamic 代码块。
        // 通过添加 optional 选项，标记该参数为可选。
        // 否则第二个 execute 部分将会作废
        dynamic(optional = true) {
            // 玩家名称补全
            suggestion<ProxyCommandSender> { sender, context -> 
                onlinePlayers().map { it.name }
            }
            execute<ProxyCommandSender> { sender, context, argument ->
                getProxyPlayer(argument)!!.sendMessage("HelloWorld")
            }
        }
        execute<ProxyCommandSender> { sender, context, argument ->
            sender.sendMessage("HelloWorld")
        }
    }

这样以来，我们便完成了对该命令的升级。输入 ``/command [玩家]`` 执行第一个 ``execute`` 部分，发送信息给该玩家，不使用参数直接输入 ``/command`` 则执行第二个 ``execute`` 部分发送信息给自己。相信你可以理解这样的结构。

现在，我需要实现 ``/command all`` 命令向所有玩家发送 ``HelloWorld`` 信息。

.. code-block:: kotlin

    command("command") {
        literal("all", optional = true) {
            execute<ProxyCommandSender> { sender, context, argument ->
                onlinePlayers().forEach { it.sendMessage("HelloWorld") }
            }
        }
        dynamic(optional = true) {
            suggestion<ProxyCommandSender> { sender, context -> 
                onlinePlayers().map { it.name }
            }
            execute<ProxyCommandSender> { sender, context, argument ->
                getProxyPlayer(argument)!!.sendMessage("HelloWorld")
            }
        }
        execute<ProxyCommandSender> { sender, context, argument ->
            sender.sendMessage("HelloWorld")
        }
    }

``literal`` 代表一个明文规定的参数，使用 ``/command all`` 将会执行这部分的逻辑。

**限制执行人**

不论是 ``execute`` 还是 ``suggestion`` 部分都需要我们定义一个泛型。它作用不仅仅是提供后续方法的补全，还有限制功能。

.. code-block:: kotlin

    execute<ProxyCommandSender> { sender, context, argument ->
        // 任何单位可执行
    }
    execute<ProxyPlayer> { sender, context, argument ->
        // 只能被玩家执行
    }
    // org.bukkit.entity.Player
    execute<Player> { sender, context, argument ->
        // 只能被玩家执行，且自动转换为 Bukkit 类型
    }

这完全避免了我们在命令开发过程中的类型判断与转换过程。

**限制参数**

第一个 ``execute`` 中，我们获取玩家时直接使用了 **非空断言**，而没有进行空指针判断。

.. code-block:: kotlin

    getProxyPlayer(argument)!!.sendMessage("HelloWorld")

因为 ``suggestion`` 代替我们进行了参数判断，在输入补全结果之外的内容将不会执行 ``execute`` 部分。若要关闭这个限制，则需要在 ``suggestion`` 中启用 ``uncheck`` 选项，不进行参数检查。

.. code-block:: kotlin

    suggestion<ProxyCommandSender>(uncheck = true) { sender, context -> 
        onlinePlayers().map { it.name }
    }

若 ``dynamic`` 参数没有提供补全，我们可以使用 ``restrict`` 结构来约束输入参数。

.. code-block:: kotlin

    dynamic {
        restrict<ProxyCommandSender> { sender, context, argument -> 
            // 只允许使用数字类型
            Coerce.asInteger(argument).isPresent
        }
    }

**嵌套结构**

无论是 ``literal`` 还是 ``dynamic`` 都属于命令结构语句，都允许嵌套使用来解释更复杂的命令。

.. code-block:: kotlin

    command("command") {
        literal("arg1") {
            literal("arg2") {
                // ...
            }
            dynamic {
                // ...
            }
        }
    }

**参数获取**

我们以 ``/var [key] [value]`` 命令为例，使用 ``/var a 1`` 设置变量 ``a`` 为 ``1``。

.. code-block:: kotlin

    command("var") {
        // 第一个参数 key 
        dynamic {
            // 第二个参数 value
            dynamic {
                execute<ProxyCommandSender> { sender, context, argument ->
                    // 这里 argument 为字符串类型，仅代表 value 参数的内容
                    // 使用 /var a 1 则此处 argument 为 "1"
                    // 因此则需要通过 context 来获取命令的上下文
                    // 通过 argument 方法取左边一个参数，这里 -1 代表 offset（偏移）而不是 index（序号）
                    val key = context.argument(-1)

                    // 若使用 /var a 11 22 33 则此处 arguemnt 为 "11 22 33"
                    // 若没有子结构，argument 会拼接后续传入的所有参数
                    val value = argument
                }
            }
        }
    }

**重写错误信息**

默认情况下，错误信息由 TabooLib 代理发送，具体表现为：

* Incorrect sender for command
* Unknown or incomplete command, see below for error
* Incorrect argument for command

分别可以通过 ``incorrectSender`` 与 ``incorrectCommand`` 方法重写。

.. code-block:: kotlin

    command("command") {
        // 错误的执行者
        incorrectSender { sender, context -> 
                
        }
        // 错误的命令
        incorrectCommand { sender, context, index, state -> 
            // index 为错误参数的位置
            // state 为错误的类型
            // 1 -> Unknown or incomplete command, see below for error
            // 2 -> Incorrect argument for command
        }
    }

简化命令注册
~~~~~~~~~~~

除使用 ``command`` 顶级函数外，还可以通过注解进行命令注册。基于 :doc:`/plugin/inject`，命令需要在单例或伴生类中定义。

.. code-block:: kotlin

    @CommandHeader("command")
    object Command {

        /**
         * 同等于：
         * command("command") {
         *     dynamic {
         *         ...
         *     }
         *     execute<ProxyCommandSender> { sender, context, argument ->
         *         ...
         *     }
         * }
         */
        @CommandBody
        val main = mainCommand {
            dynamic {
                suggestion<ProxyCommandSender> { sender, context -> 
                    onlinePlayers().map { it.name }
                }
                execute<ProxyCommandSender> { sender, context, argument ->
                    getProxyPlayer(argument)!!.sendMessage("HelloWorld")
                }
            }
            execute<ProxyCommandSender> { sender, context, argument ->
                sender.sendMessage("HelloWorld")
            }
        }
        
        /**
         * 同等于：
         * command("command") {
         *     literal("all", optional = true) {
         *         ...
         *     }
         * }
         */
        @CommandBody(optional = true)
        val all = subCommand {
            execute<ProxyCommandSender> { sender, context, argument ->
                onlinePlayers().forEach { it.sendMessage("HelloWorld") }
            }
        }
    }

相比标准命令注册方式，这样省去了定义 ``@Awake`` 的过程，使项目更加有序且规范。