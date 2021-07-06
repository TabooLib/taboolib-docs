===========
设置 Gradle
===========

使用 `TabooLibGradle <https://github.com/TabooLib/taboolib-gradle-plugin>`_ 非常简单，它除了提供一些必要的功能外，还提供了对插件元数据的集成，自动生成各平台插件运行时所需要的信息文件。

下面是一个可以用于 ``Bukkit`` 平台插件的一个简单模板，别忘记把 ``group`` 替换成你的包名。

.. code-block:: groovy

    plugins {
        id 'java'
        id 'io.izzel.taboolib' version '1.7'
        id 'org.jetbrains.kotlin.jvm' version '1.5.10'
    }

    group = 'com.example'
    version = '1.0.0-SNAPSHOT'

    taboolib {
        descriptionFile {
            author '坏黑'
        }
        install 'common'
        install 'platform-bukkit'
        version '6.0.0'
    }

    repositories {
        mavenCentral()
    }

    dependencies {
        implementation 'ink.ptms.core:v11605:11605'
        implementation 'org.jetbrains.kotlin:kotlin-stdlib'
    }

.. note::

    你的插件名称在 ``settings.gradle`` 文件中设置。

你可以在 ``taboolib`` 选项中安装所需要的 :doc:`module` 和设置 TabooLib 版本。或是针对 :doc:`plugin-meta` 进行更详细的设置。例如这这样修改可以添加在 ``Bukkit`` 平台运行所需的插件依赖。

.. code-block:: groovy

    taboolib {
        descriptionFile {
            author '坏黑'
            depend 'Adyeshach'
        }
    }