==================
设置 IntelliJ IDEA
==================

这部分解释了如何为开发基于 TabooLib 的插件设置你的 IntelliJ IDEA 工作目录。

创建项目
========

* 打开 **IntelliJ IDEA**。
* 点击 ``New Project``。
* 在弹出的窗口中选择 ``Gradle``。
* 点选 ``Kotlin/JVM`` 框架。
* 确保你的 **Project SDK** 选项中选择了 Java 8/1.8 或者更高版本。
* 点击 ``Next``。
* 在 ``Name`` 中输入项目名称，在 ``Location`` 中输入项目所在目录。
* 展开 ``Artifact Coordinates`` 隐藏选项。
* 在 ``GroupId``，``ArtifactId``，``Version`` 分别输入项目信息。

  *  你的 ``GroupId`` 应当和你的包名保持一致，详见 :doc:`/plugin/main`。
  *  你的 ``ArtifactId`` 应当和你的插件名保持一致，例如 ``myplugin``。
  *  你的 ``Version`` 版本号由你决定，可以参考 :doc:`/plugin/project/version`。

* 点击 ``Finish``。
* 插件项目新建完成后，此时应该会有 ``/src/main/java`` 目录自动生成完毕，你在这个目录里可以开始写插件了。

编辑构建脚本
============

* 打开 ``build.gradle`` 文件。
* 根据 :doc:`/plugin/project/gradle` 中的内容编辑构建脚本。
* 在 **IntelliJ IDEA** 的右侧展开 **Gradle** 选项卡并点击刷新按钮。
* Gradle 相关的设置就已经完成了！

调试插件
========

下述流程可以用来快速调试插件，但并不适合快速迭代开发。

* 在 **IntelliJ IDEA** 的右侧展开 **Gradle** 选项卡并依次点击 ``Tasks`` -> ``build`` -> ``build``。
* 随后在 ``build/libs`` 目录中便可以看到你的插件。

将构建出的 jar 文件复制到可以运行的服务器重的插件文件夹中，重启服务器以测试。

导入项目
========

假如你使用的是 `TabooLib SDK <https://github.com/taboolib/taboolib-sdk>`_ 进行插件开发，那么你需要的是直接导入而不是在 IDE 中创建。

* 打开 **IntelliJ IDEA**。
* 点击 ``Open``。
* 选择你下载的 TabooLib SDK 目录中的 ``build.gradle`` 文件。

Git 集成
=========

JetBrains 提供了详细的使用他们的 Git 集成的文档：

https://www.jetbrains.com/help/idea/using-git-integration.html