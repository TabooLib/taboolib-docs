=======================
搭建 TabooLib 测试环境
=======================

TabooLib
==========

从 `TabooLib 仓库 <https://github.com/Bkm016/TabooLib>`_ 中克隆完整项目在你的工作环境中。将 ``build.gradle.kts`` 构建文件中的发布仓库地址改为你的 **本地仓库** 或是 **任意本地目录** 如下所示。

.. code-block:: kotlin

    publishing {
        repositories {
            maven {
                url = uri("/Users/sky/Desktop/repo")
            }
        }
    }

随后输入以下命令完成构建及本地发布。

.. code-block:: bash

    ./gradlew build publish


TabooLib Test Units
=====================

从 `TabooLib Test Units 仓库 <https://github.com/Bkm016/TabooLib-Test-Units>`_ 中克隆测试项目在你的工作环境中。将 ``build.gradle`` 构建文件中的仓库地址改为你的刚才设置的地址，如下所示。

.. code-block:: groovy

    repositories {
        maven {
            url uri("/Users/sky/Desktop/repo")
        }
        mavenCentral()
    }

随后输入以下命令完成构建。

.. code-block:: bash
    
    ./gradlew build