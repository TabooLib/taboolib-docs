========
监控器
========

简易的性能损耗监控，表现形式如下所示。所有操作均是线程安全的。

.. image:: /images/Xnip2021-10-11_16-53-00.png

具体使用方式如下形式：

.. code-block:: kotlin

    mirrorNow("onTick") {
        // 该方法体的运行结果会返回给 mirrorNow 方法
    }

    mirrorFuture<Int>("onTick") {
        // ...
        // 使用 finish 方法停止监控，并返回给定内容
        finish(0)
    }

    command("report") {
        execute<ProxyCommandSender> { sender, _, _ ->
            // 打印统计结果
            Mirror.report(sender)
        }
    }