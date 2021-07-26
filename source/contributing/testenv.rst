=======================
搭建 TabooLib 测试环境
=======================

在向 TabooLib 贡献代码的过程中我们经常需要进行本地测试，但是我们不能将测试版本发布到 TabooLib 远程仓库。所以我们需要搭建本地测试环境，并向发布到本地以供我们后续测试时使用。

从 `TabooLib 仓库 <https://github.com/Bkm016/TabooLib>`_ 中克隆完整项目在你的工作环境中。将 ``build.gradle.kts`` 构建文件中的发布仓库地址改为你的 **本地仓库** 如下所示。

.. code-block:: kotlin

    publishing {
        repositories {
            mavenLocal()
        }
    }

随后输入以下命令完成构建及本地发布。不过不要忘记修改版本号，不能是已经发布的版本。

.. code-block:: bash

    ./gradlew build publish

届时你便可以在你的测试项目中添加 **本地仓库** 来获取刚才发布的 TabooLib 版本。

.. code-block:: groovy

    repositories {
        mavenLocal()
    }

随后输入以下命令完成构建。

.. code-block:: bash
    
    ./gradlew build