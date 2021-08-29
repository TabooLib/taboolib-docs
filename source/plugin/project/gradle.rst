===========
设置 Gradle
===========

使用 `TabooLibGradle <https://github.com/TabooLib/taboolib-gradle-plugin>`_ 非常简单，它除了提供一些必要的功能外，还提供了对插件元数据的集成，自动生成各平台插件运行时所需要的信息文件。

下面是一个可以用于 ``Bukkit`` 平台插件的一个简单模板，别忘记把 ``group`` 替换成你的包名。

.. code-block:: kotlin

    plugins {
        java
        // 不可低于 1.25 版本
        id("io.izzel.taboolib") version "1.25"
        // 基于 TabooLib Runtime Env 你可以使用任何版本的 Kotlin 环境
        id("org.jetbrains.kotlin.jvm") version "1.5.10"
    }

    taboolib {
        description {
            contributors {
                name("坏黑").description("TabooLib Developer")
            }
        }
        install("common")
        install("platform-bukkit")
        version = "6.0.0-pre57"
    }

    repositories {
        mavenCentral()
    }

    dependencies {
        compileOnly("ink.ptms.core:v11701:11701:mapped")
        compileOnly("ink.ptms.core:v11701:11701:universal")
        compileOnly(kotlin("stdlib"))
        compileOnly(fileTree("libs"))
    }

.. note::

    插件的 :doc:`identifier` 在 ``settings.gradle`` 文件中设置。

你可以在 ``taboolib`` 选项中安装所需要的 :doc:`module` 和设置 TabooLib 版本。或是针对 :doc:`/plugin/plugin-meta` 进行更详细的设置。例如这这样修改可以添加在 ``Bukkit`` 平台运行所需的插件依赖。

.. code-block:: kotlin

    taboolib {
        description {
            contributors {
                name("坏黑").description("TabooLib Developer")
            }
            dependencies {
                name("Chemdah")
                name("Adyeshach").optional(true)
            }
        }
    }

**版本隔离**

为了解决 Kotlin 的版本冲突问题，TabooLib 在编译插件时会对所有 Koltin 引用进行重定向。例如 ``koltin.Lazy`` 将会被重定向到 ``kotlin1510.Lazy``，这里的 ``1510`` 代表 kotlin ``1.5.10`` 版本。通过 ``options`` 选项来修改这一过程。

·· code-block: kotlin

    taboolib {
        // 不对 Kotlin 进行重定向，且不下载 Kotlin 标准库。
        options("skip-kotlin")
    }
    
·· code-block: kotlin

    taboolib {
        // 不对 Kotlin 进行重定向
        options("skip-kotlin-relocate")
    }

·· code-block: kotlin

    taboolib {
        // 移除 Runtime Env 部分代码，不建议使用
        options("skip-env")
    }