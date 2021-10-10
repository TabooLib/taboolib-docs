=========
阻断器
=========

用于阻挡频繁发生的事件，并对其施加冷却时间。具体表现在 ``taboolib.common5.Baffle`` 类中。

.. code-block:: java

    /**
     * 按时间阻断
     * 单位：毫秒
     *
     * @param duration 时间数值
     * @param timeUnit 时间单位
     * @return {@link Baffle}
     */
    @NotNull
    public static Baffle of(long duration, TimeUnit timeUnit)

    /**
     * 按次阻断（类似 SimpleCounter）
     *
     * @param count 次数
     * @return {@link Baffle}
     */
    @NotNull
    public static Baffle of(int count)

    /**
     * 重置所有数据
     */
    public void resetAll();

    /**
     * 重置个体的执行缓存
     *
     * @param id 个体序号
     */
    public void reset(String id);

    /**
     * 强制个体更新数据
     *
     * @param id 个体序号
     */
    public void next(String id);

    /**
     * 验证个体的执行结果
     *
     * @param id     个体序号
     * @param update 是否更新数据
     * @return 是否运行
     */
    public boolean hasNext(String id, boolean update);

    /**
     * 同 {@link Baffle#next(String)}，个体序号为（*）
     */
    public void reset();

    /**
     * 同 {@link Baffle#next(String)}，个体序号为（*）
     */
    public void next();

    /**
     * 同 {@link Baffle#hasNext(String, boolean)}，个体序号为（*）
     *
     * @return 是否运行
     */
    public boolean hasNext();

    /**
     * 同 {@link Baffle#hasNext(String, boolean)}
     *
     * @param id 个体序号
     * @return 是否运行
     */
    public boolean hasNext(String id);

具体使用方式如下所示：

.. code-block:: kotlin

    object Listener {
        
        /**
         * 声明一个周期为 10 秒的阻断器
         */
        val baffle1 = Baffle.of(10, TimeUnit.SECONDS)

        @SubscribeEvent
        fun onClick(event: PlayerInteractEvent) {
            // 判断玩家是否通过阻断器的等待时间
            // 若玩家在 10 秒内再次触发该事件则结果为否
            if (baffle1.hasNext(event.player.name)) {
                // ...
            }
        }

        @SubscribeEvent
        fun onQuit(event: PlayerQuitEvent) {
            // 当玩家离开服务器时需释放缓存，否则将会造成内存溢出
            baffle1.reset(event.player.name)
        }
    }