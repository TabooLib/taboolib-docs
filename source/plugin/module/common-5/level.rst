===========
经验计算器
===========

用于计算原版等级和经验，具体表现在 ``taboolib.common5.Level`` 类中。

.. code-block:: java

    /**
     * 设置玩家的当前经验总值
     *
     * @param player 玩家
     * @param exp 经验
     */
    public static void setTotalExperience(ProxyPlayer player, int exp);
    
    /**
     * 获取当前等级下的最大经验
     * 根据运行平台分为 Bukkit 和 Nukkit 两种不同的算法
     * 
     * @param level 等级
     */
    public static int getExpAtLevel(int level);
    
    /**
     * 获取当前等级下的最大经验总值（从 1 级到该等级的所有最大经验总和）
     *
     * @param level 等级
     */
    public static int getExpToLevel(int level);

    /**
     * 获取玩家当前经验总值
     * 
     * @param player 玩家
     */
    public static int getTotalExperience(ProxyPlayer player);

    /**
     * 获取玩家距离升级还差多少经验
     * 
     * @param player 玩家
     */
    public static int getExpUntilNextLevel(ProxyPlayer player);