===========
安装 Gradle
===========

Gradle 是一个基于 JVM 的构建工具，所有基于 TabooLib 的插件必须在 Gradle 工具下开发。

在 `Gradle 主页 <https://gradle.org>`__ 中可以找到大量的文档，以及一系列适用于不同操作系统的 Gradle 环境安装方法。

下载
=====

需要注意的是在安装 Gradle 之前必须安装 JDK/JRE 7 以上版本。在控制台输入 ``java -version`` 可以看到当前计算机所安装的 Java 版本信息。

在 `Gradle 分发页面 <https://gradle.org/releases/>`_ 下载最新的 Gradle 发行包。

.. image:: /images/1596702551777608.png

解压
====

Gradle 发行包是一个 Zip 压缩文件，将压缩文件解压到你想要安装的目录。

环境变量
========

解压文件后还需要对计算机环境变量进行修改。

Windows 平台
~~~~~~~~~~~~

新建变量

.. csv-table::
   :header: "变量名", "变量值"
   :widths: 1, 2

   "GRADLE_HOME", "Gradle 发行包所解压的目录，例如: ``D:\Java\gradle-6.5.1``"
   "GRADLE_USER_HOME", "Gradle 自定义仓库目录，例如: ``D:\Java\repository``。这个选项是可选的。"

.. image:: /images/faf87bc44c064b7d3a2fd230f61800e4.png

.. image:: /images/4452ec02e17e8d59775c7391471af181.png

添加变量

.. csv-table::
   :header: "变量名", "变量值"
   :widths: 1, 2

   "Path", "%GRADLE_HOME%\bin;"

.. image:: /images/8b4555785af3e3f51eece0258da89e7e.png

macOS 平台
~~~~~~~~~~

在终端中输入

.. code-block:: bash

   open -e .bash_profile

打开 ``.bash_profile`` 文件后并在文件中输入以下内容

.. code-block:: profile

   GRADLE_HOME=/Users/sky/Desktop/gradle-6.5.1
   export GRADLE_HOME
   export PATH=$PATH:$GRADLE_HOME/bin

.. note::

   将 ``GRADLE_HOME`` 的值替换成你的 Gradle 发行包所解压的目录

保存 ``.bash_profile`` 文件并在终端中执行以下命令来更新 ``.bash_profile`` 文件。

.. code-block:: bash

   source ~/.bash_profile

Linux 和 Unix 平台
~~~~~~~~~~~~~~~~~~~
   
在终端中输入
   
.. code-block:: bash
   
   vi /etc/profile.d/gradle.sh
   
打开 ``profile`` 文件后并在文件中输入以下内容
   
.. code-block:: profile
   
   export GRADLE_HOME=/opt/software/gradle-6.5.1
   export PATH=$PATH:$GRADLE_HOME/bin
   export GRADLE_USER_HOME=/opt/.gradle
   
.. note::
   
   将 ``GRADLE_HOME`` 的值替换成你的 Gradle 发行包所解压的目录
   
保存 ``profile`` 文件并在终端中执行以下命令来更新 ``profile`` 文件。
   
.. code-block:: bash
   
   source /etc/profile

测试安装
========

运行如下命令来检查是否安装成功，并显示当前的 Java 版本和 Gradle 版本。

.. code-block:: bash

   gradle -v 
