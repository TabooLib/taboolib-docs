========
开放接口
========

开放接口一般用于模块开发，在不同插件之间传递数据、执行方法。TabooLib 中的 Kether 便是基于开放接口。

.. tips::

    开放接口的前身为 openapi.xxx 这样的包名，被海螺先生嘲讽过。

顶级函数
~~~~~~~~

.. code-block:: kotlin

    /**
    * 获取当前服务端中运行的所有开放接口
     */
    fun getOpenContainers(): List<OpenContainer>

    /**
     * 获取特定名称的开放接口
     */
    fun getOpenContainer(name: String): OpenContainer?

注册开放接口
~~~~~~~~~~~

用于接收开放接口调用请求，依赖 ``@Awake`` 注解自动注册。

.. code-block:: kotlin

    @Awake
    object MyListener : OpenListener {

        override fun call(name: String, data: Array<Any>): OpenResult {
            return OpenResult.failed()
        }
    }

使用开放接口
~~~~~~~~~~~

代码节选自 ``kether`` 模块。

.. code-block:: kotlin

    getOpenContainers().forEach {
        it.call(StandardChannel.REMOTE_ADD_ACTION, arrayOf(pluginId, annotation.value, annotation.namespace))
    }