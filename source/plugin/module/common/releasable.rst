=======
释放器
=======

在插件卸载时运行 ``release`` 方法，用于资源释放，依赖 ``@Awake`` 注解自动注册。

代码节选自 ``common-5`` 模块。

.. code-block:: java

    @Awake
    public class FileWatcher implements Releasable {

        ...

        @Override
        public void release() {
            unregisterAll();
        }
    }