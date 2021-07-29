=========
项目架构
=========

TabooLib ``6.0`` 由多个子模块构成，统一存放在 TabooLib 仓库中。大致如下：

.. csv-table::
   :header: "模块", "说明"
   :widths: 3, 7
   
   "common", "TabooLib 的核心部分，环境部署以及跨平台接口"
   "common-5", "TabooLib 5.0 版本保留下来的一些工具"
   "module-ai", "管理与注册自定义实体 AI（Pathfinder）"
   "module-chat", "Component（Json）信息构建工具与 1.16 RGB 颜色转换"
   "module-configuration", "Yaml 封装接口与配置文件管理工具"
   "module-database", "数据库管理工具"
   "module-database-mongodb", "数据库管理工具（MongoDB）"
   "module-effect", "粒子生成工具"
   "module-kether", "内建脚本（动作语句）解决方案"
   "module-lang", "语言文件工具"
   "module-metrics", "bStats 整合"
   "module-navigation", "无实体寻路工具"
   "module-nms", "跨版本 nms 解决方案与数据包管理工具"
   "module-nms-util", "常用 nms 工具集合"
   "module-porticus", "BungeeCord 通讯工具"
   "module-ui", "箱子菜单构建工具"
   "module-ui-receptacle", "箱子菜单构建工具（发包实现）"
   "platform-bukkit", "Bukkit 实现"
   "platform-bungee", "BungeeCord 实现"
   "platform-nukkit", "Nukkit 实现"
   "platform-sponge-api7", "Sponge (api7) 实现"
   "platform-sponge-api8", "Sponge (api8) 实现"
   "platform-velocity", "Velocity 实现"
