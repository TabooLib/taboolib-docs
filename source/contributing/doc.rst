===========
帮助撰写文档
===========

TabooLibDocs 是 TabooLib 项目的官方文档。旨在帮助开发者们了解 TabooLib 插件开发的相关信息，并为有意向 TabooLib 贡献代码的开发者指明方向。

报告问题
========

然而文档难免会有疏漏，诸如过期内容或是错别字，亦或你觉得 "某个地方这样说更好"。如果你遇到了这样的情况，但你因为种种原因无法直接为我们提供帮助，我们仍然留有四条反馈的途径：

1. 在 `TabooLibDocs 位于 GitHub 的问题追踪器 <https://github.com/TabooLib/TabooLibDocs/issues>`_ 中反馈
2. 在我们的讨论群 ``809083692`` 中找到我们。

撰写文档
========

对 TabooLibDocs 任何形式的变动都应当通过 `TabooLibDocs 位于 GitHub 的仓库 <https://github.com/TabooLib/TabooLibDocs>`_ 完成。我们并不期望你的 Pull Request 从一开始就是完美的，绝大部分 Pull Request 也都会在复核时得到进一步完善；甚至我们还欢迎不完整的解释，所以不要因为你有地方搞不明白而感到害怕；总会有人协助填补空白的。

为确保所有 TabooLibDocs 页面的排版一致性，在遇到特定类型的代码块时，应使用下列代码。

    * Groovy/Gradle 文件 -> ``groovy``
    * HOCON 配置文件 -> ``guess``（暂不支持 HOCON 语法高亮）
    * 游戏内或服务器终端命令 -> ``none``
    * Java 代码 -> ``java``
    * Json 格式的配置文件 -> ``json``
    * Linux 终端命令 -> ``bash``
    * 日志 -> ``none``
    * 纯文本 -> ``text``
    * Windows 命令行 -> ``bat``