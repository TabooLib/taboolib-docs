=======
调度器
=======

每个平台都有调度器（Scheduler）部分，但 TabooLib 自身不管理调度器。不同的平台对于调度器的定义有所不同，但大致作用相同，均在服务器完全启动后开始执行。

注册调度器
~~~~~~~~~

通过顶级函数 ``submit`` 进行调度器注册，该函数中所有参数均为可选。

.. code-block:: kotlin

    // 创建一个只运行 1 次的调度器，在服务器完全启动后向控制台打印 HelloWorld 信息
    submit {
        println("HelloWorld")
    }

    // 创建一个只运行 1 次的调度器，在 5 游戏刻后启动
    submit(delay = 5) {
        // ...
    }

    // 创建一个循环调度器，每 20 游戏刻运行一次
    submit(period = 20) {
        // ...
    }

    // 创建一个循环调度器，每 20 游戏刻运行一次，在 5 游戏刻后启动
    submit(period = 20, delay = 5) {
        // ...
    }

    //  创建一个只运行 1 次的调度器，在非主线程中运行
    submit(async = true)) {
        // ...
    }

**注销调度器**

无论是在调度器的内部还是外部，都可以通过 ``cancel`` 方法来注销。

.. code-block:: kotlin

    submit {
        // 注销方法并不会影响本次运行，而是在本次运行结束后停止调度器
        cancel()
    }

    val task = submit {
        // ...
    }
    task.cancel()

绑定到方法
~~~~~~~~~~

除使用 ``submit`` 顶级函数外，还可以通过注解进行调度器注册。基于 :doc:`/plugin/inject`，调度器需要在单例或伴生类中定义。

.. code-block:: kotlin

    object MySchedule {

        @Schedule(period = 1)
        fun onTick() {
            // ...
        }
    }

.. warning::

    由 ``@Schedule`` 注册的调度器无法被注销，直到插件卸载。

同步执行器
~~~~~~~~~~

在多线程开发工作中，常常需要返回主线程获取数据，如一些地图数据必须在主线程中获取。在 Bukkit 平台中可以使用 ``callSyncMethod`` 这类方法，但是并不理想。

.. code-block:: kotlin

    // 非主线程
    submit(async = true) {
        ...
        val data = sync { world.anySyncMethod() }
        ...
    }

通过 ``sync`` 方法快速切回主线程，并将运行结果返回。