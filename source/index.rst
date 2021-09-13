======================
TabooLib 开发文档
======================

前言
========

欢迎来到 TabooLibDocs。这里定义了基于 `TabooLib <https://github.com/TabooLib/TabooLib>`__ ``6.0`` 编写 Minecraft 插件而提供的指导性准则和建议。

TabooLib 是基于多种 Minecraft 服务端平台的插件开发框架，你可以在 **原生** 的 Bukkit 平台运行基于 TabooLib 编写的插件，同样这个插件也可以在 Sponge、Nukkit 等平台运行。你可以在 :doc:`这里 <versions/index>` 查看 TabooLib 的版本信息并下载 `SDK <https://github.com/taboolib/taboolib-sdk>`_ 快速开始。

TabooLib 自 ``6.0`` 版本起不再是 **动态下载** 模式，而是改为由依赖插件自行打包并随本体同时载入的纯类库形式。这极大程度的提升了插件的稳定性和安全性，正因如此 TabooLib 的所有工具也在这个版本进行了全面重新设计。整个库被拆分为数个模块，由这些模块共同组成 TabooLib ``6.0``，你可以在 :doc:`这里 <about/structure>` 了解模块之间的结构与相关信息，或直接访问我们的 `Github <https://github.com/taboolib>`_ 仓库。

本文档是基于 `SpongeDocs <https://docs.spongepowered.org>`_ 二次开发的离线版本。

.. note::

    TabooLib ``6.0`` 还在实验阶段，
    我希望更多开发者能够加入我们，为我们提供有效建议和帮助。

内容
=======

版本信息
~~~~~~~~

这部分用于表示 TabooLib 如何控制各个版本，以及与旧版本之间的关系。

.. toctree::
    :maxdepth: 2
    :titlesonly:

    versions/index

准备工作
~~~~~~~~

首先确保你的计算机已经联网！并在这部分后阅读 :doc:`plugin/index` 和 :doc:`contributing/index`。

.. toctree::
    :maxdepth: 2
    :titlesonly:

    preparing/index

创造插件
~~~~~~~~

现在我们将开始编写基于 TabooLib 的跨平台 Minecraft 服务器插件。

.. toctree::
    :maxdepth: 5
    :titlesonly:

    plugin/index

向 TabooLib 贡献代码
~~~~~~~~~~~~~~~~~~~~

想让 TabooLib 变得更加优秀或是添加更多你想要的工具？

.. toctree::
    :maxdepth: 2
    :titlesonly:

    contributing/index

关于 TabooLib 项目
~~~~~~~~~~~~~~~~~~

这部分包含了 TabooLib 的基本信息，如果你感到对这个项目感到困惑可以看看这里。

.. toctree::
    :maxdepth: 3
    :titlesonly:

    about/index

链接
====

.. toctree:: 
    :maxdepth: 2
    :titlesonly:

-  `TabooLib 我的世界中文论坛 <https://www.mcbbs.net/thread-773065-1-1.html>`_
-  `TabooLib 仓库 <https://github.com/TabooLib>`_
-  `TabooLib SDK <https://github.com/TabooLib/TabooLib-SDK>`_
-  `TabooLib 问题反馈 <https://github.com/TabooLib/TabooLib/issues?q=>`_
-  `TabooLib Javadocs <https://jd.tabooproject.org>`_
-  `Sponge 主页 <https://www.spongepowered.org>`_
-  `Sponge 文档 <https://docs.spongepowered.org>`_