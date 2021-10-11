==========
时间计算器
==========

时间计算器具体表现为 ``taboolib.common5.ReadTime`` 和 ``taboolib.common5.TimeCycle`` 两个工具。他们的作用均为通过特定单位获取未来的某个时间，但作用存在细微的差别。具体用法如下所示：

RealTime
~~~~~~~~~

通过当前时间推算未来时间

.. code-block:: kotlin
    
    // START_IN_SUNDAY 表示周日是每周的开始，周六结束
    // START_IN_MONDAY 表示周一是每周的开始，周日结束
    // 获取从现在起的 2 小时后，分钟及以下单位取 0
    // 输入: 03:30:01.300
    // 输出: 05:00:00.000
    RealTime.START_IN_SUNDAY.nextTime(RealTime.Type.HOUR, 2)
    
    // 获取从现在起的 3 天后，小时及以下单位取 0
    // 输出: 2021/10/11 12:30:01.300
    // 输出: 2021/10/14 00:00:00.000
    RealTime.START_IN_SUNDAY.nextTime(RealTime.Type.DAY, 3)

TimeCycle
~~~~~~~~~~~

通过给定时间推算下一周期时间

.. code-block:: kotlin

    // 解析字符串为 TimeCycle 对象
    // 每天 6 点
    val cycle = "day 6".parseTimeCycle()
    // 设定起始时间为当前时间
    cycle.start(System.currentTimeMillis())
    // 判断起始时间是否超过今日 6 点
    // 输入: 05:00, 输出: 否
    // 输入: 07:00, 输出: 是
    if (cycle.isTimeout) {
        // ...
    }

受 ``String.parseTimeCycle()`` 方法支持的时间单位有 ``day``, ``week``, ``month``。具体表现形式如下：

.. code-block:: yaml

    meta:
      # 当日或次日 6 点后超时
      # 可用：day（日）week（周）month（月）
      # week 01 06 00
      # month 01 06 00
      timeout: day 06 00

除此之外还可以使用构造函数来代替 ``String.parseTimeCycle()`` 方法。

.. code-block:: java

    /**
     * 时间长度（毫秒）
     * 使用该构造器则不使用时间周期，而使用特定时间长度。
     * 例如 10 分钟、30 秒。
     */
    public TimeCycle(long time);

    /**
     * 使用 DAY 类型创建时间周期
     */
    public TimeCycle(int hour, int minute);

    /**
     * 使用 WEEK 或 MONTH 创建时间周期
     */
    public TimeCycle(Type type, int day, int hour, int minute);

.. tips::

    Chemdah 同时使用了这两种时间工具来实现 automation 与 timeout 组件。