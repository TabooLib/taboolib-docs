==================
TabooLib 项目架构
==================

TabooLib ``6.0`` 由多个子模块构成，统一存放在 TabooLib 仓库中。大致如下：

.. csv-table::
   :header: "模块", "说明", "依赖"
   :widths: 1, 3, 1
   
   "common", "TabooLib 的核心部分，环境部署以及跨平台接口", "无"
   "common-5", "TabooLib 5.0 版本保留下来的一些工具", "common"
   "module-ai", "管理与注册自定义实体 AI（Pathfinder）", "module-nms"
   "module-chat", "Component（Json）信息构建工具与 1.16 RGB 颜色转换", "common"
   "module-configuration", "Yaml 封装接口与配置文件管理工具", "common-5"
   "module-database", "数据库管理工具", "module-configuration"
   "module-effect", "粒子生成工具", "common"
   "module-kether", "内建脚本（动作语句）解决方案", "common-5, module-configuration"
   "module-lang", "语言文件工具", "common-5, module-configuration"
   "module-metrics", "bStats 整合", "module-configuration"
   "module-navigation", "无实体寻路工具", "module-nms"
   "module-nms", "跨版本 nms 解决方案", "platform-bukkit"
   "module-nms-util", "复合 nms 工具", "module-nms"
   "module-porticus", "BungeeCord 通讯工具", "platform-bukkit, platform-bungee"
   "module-ui", "箱子菜单构建工具", "platform-bukkit"
   "module-ui-receptacle", "箱子菜单构建工具（发包）", "module-nms"
   "platform-bukkit", "Bukkit 实现", "common"
   "platform-bungee", "BungeeCord 实现", "common"
   "platform-nukkit", "Nukkit 实现", "common"
   "platform-sponge-api7", "Sponge (api7) 实现", "common"
   "platform-sponge-api8", "Sponge (api8) 实现", "common"
   "platform-velocity", "Velocity 实现", "common"