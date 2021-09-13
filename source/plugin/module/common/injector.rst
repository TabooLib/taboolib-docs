=====
注入
=====

是 :doc:`/plugin/inject` 的底层实现，具体表现在三个接口：

* Injector.Classes
* Injector.Fields
* Injector.Methods

分别用于类、字段和方法。

注册注入器
~~~~~~~~~

代码节选自 ``common`` 模块，依赖 ``@Awake`` 注解自动注册。

.. code-block:: kotlin

    @Awake
    object ScheduleLoader : Injector.Methods {

        /**
         * 优先级
         */
        override val priority: Byte
            get() = 0

        /**
         * 在什么生命周期阶段下注入
         */
        override val lifeCycle: LifeCycle
            get() = LifeCycle.ACTIVE

        /**
         * 具体方法
         */
        override fun inject(method: Method, clazz: Class<*>, instance: Supplier<*>) {
            // 是否存在 @Schedule 注解
            if (method.isAnnotationPresent(Schedule::class.java)) {
                val schedule = method.getAnnotation(Schedule::class.java)
                val obj = instance.get()
                submit(async = schedule.async, delay = schedule.delay, period = schedule.period) { method.invoke(obj) }
            }
        }
    }