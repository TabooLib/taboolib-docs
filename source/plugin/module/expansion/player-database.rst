==========
玩家数据库
==========

使用该扩展快速部署 SQL & SQLite 玩家数据库。

**该模块依赖于：**

* common
* module-database

**数据结构如下所示：**

.. code-block:: javascript

    {
        "bukkitObj": {
            "health": "20"
            "x": 10
            "y": 0
            "z": 10
        },
        "kirraObj": {
            "health": "20"
            "x": 10
            "y": 0
            "z": 10
        }
    }

每个玩家拥有一个独立 Map 容器，键值类型均为可变长度字符串，最大长度 64 字节。

SQL
~~~~~

使用配置文件加载 SQL 类型玩家数据库，表现形式如下：

.. code-block:: yaml

    database:
      host: localhost
      port: 3306
      user: root
      password: root
      database: root
      table: my_database

.. code-block:: kotlin

    @Config
    lateinit var conf: SecuredFile
        private set

    override fun onEnable() {
        // 初始化玩家容器数据库，若数据库连接失败该方法会抛出异常
        setupPlayerDatabase(conf.getConfigurationSection("database"))
    }

SQLite
~~~~~~~

加载 SQLite 类型玩家数据库，表现形式如下：

.. code-block:: kotlin

    override fun onEnable() {
        // 初始化玩家容器数据库，若数据库连接失败该方法会抛出异常
        setupPlayerDatabase(File(getDataFolder(), "data.db"))
    }

混合写法
~~~~~~~~

.. code-block:: kotlin

    override fun onEnable() {
        // 使用配置文件判断玩家数据库类型
        if (conf.getBoolean("database.enable")) {
            setupPlayerDatabase(conf.getConfigurationSection("database"))
        } else {
            setupPlayerDatabase(newFile(getDataFolder(), "data.db"))
        }
    }

使用方式
~~~~~~~~

在服务器启动时必须通过 `setupPlayerDatabase` 方法初始化数据库，否则将无法进行接下来的行为：

.. code-block:: kotlin

    @SubscribeEvent
    fun e(e: PlayerJoinEvent) {
        // 初始化玩家容器
        e.player.setupDataContainer()
        // 读取或写入数据（写入时唤起异步 I/O 任务，尽量避免高频写入）
        e.player.getDataContainer()["test"] = 123
    }

    @SubscribeEvent
    fun e(e: PlayerQuitEvent) {
        // 释放玩家容器缓存
        e.player.releaseDataContainer()
    }
